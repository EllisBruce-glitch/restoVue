<template>
    <HeaderComponent />

    <h1>Hello {{ name }}, Welcome to Add Restaurant Page</h1>
    <form class="add">
        <input type="text" name="name" placeholder="Enter Name" v-model="restaurant.name" />
        <input type="text" name="address" placeholder="Enter Address" v-model="restaurant.address" />
        <input type="text" name="contact" placeholder="Enter Contact" v-model="restaurant.contact" />
        <button type="button" v-on:click="addRestaurant"> Add New Restaurant</button>
    </form>
</template>

<script>

import HeaderComponent from './HeaderComponent.vue'
import axios from 'axios';

export default {
    name: 'AddResto',

    data() {
        return {
            restaurant: {
                name: '',
                address: '',
                contact: ''
            }

        };
    },

    components: {
        HeaderComponent
    },

    methods: {
        async addRestaurant() {
            console.warn(this.restaurant)
            let result = await axios.post("http://localhost:3000/restaurants", {
                name: this.restaurant.name,
                address: this.restaurant.address,
                contact: this.restaurant.contact,
            });
            if (result.status == 201) {
                this.$router.push({ name: "HomePage" })
            }
            console.warn(result)
        }
    },


    mounted() {
        let user = localStorage.getItem('user-info');
        this.name = JSON.parse(user)[0].name;
        if (!user) {
            this.$router.push({ name: 'SignUp' })
        }
    }
}

</script>

<style scoped>
.add>input {
    width: 300px;
    height: 40px;
    padding-left: 20px;
    display: block;
    margin-bottom: 30px;
    margin-right: auto;
    margin-left: auto;
    border: 1px solid #373e45;
}

.add>button {
    width: 320px;
    height: 40px;
    border: 1px solid #373e45;
    background-color: #373e45;
    color: #fff;
    cursor: pointer;
}
</style>