<template>
    <HeaderComponent />

    <h1>Hello {{ name }}, Welcome to Update Restaurant Page</h1>
    <form class="update">
        <input type="text" name="name" placeholder="Enter Name" v-model="restaurant.name" />
        <input type="text" name="address" placeholder="Enter Address" v-model="restaurant.address" />
        <input type="text" name="contact" placeholder="Enter Contact" v-model="restaurant.contact" />
        <button type="button" v-on:click="updateRestaurant"> Update Restaurant</button>
    </form>
</template>

<script>

import HeaderComponent from './HeaderComponent.vue'
import axios from 'axios';

export default {
    name: 'UpdateResto',

    data() {
        return {
            restaurant: {
                name: '',
                address: '',
                contact: ''
            }

        };
    },

    methods: {
        async updateRestaurant() {

            console.warn(this.restaurant)
            let result = await axios.put("http://localhost:3000/restaurants/" + this.$route.params.id, {
                name: this.restaurant.name,
                address: this.restaurant.address,
                contact: this.restaurant.contact,
            });
            if (result.status == 200) {
                this.$router.push({ name: "HomePage" })
            }
            console.warn(result)
        }
    },

    components: {
        HeaderComponent
    },
    async mounted() {
        let user = localStorage.getItem('user-info');
        this.name = JSON.parse(user)[0].name;
        if (!user) {
            this.$router.push({ name: 'SignUp' })
        }

        let result = await axios.get("http://localhost:3000/restaurants/" + this.$route.params.id)

        console.warn(this.$route.params.id)
        console.warn(result)
        this.restaurant = result.data


    }
}

</script>


<style scoped>
.update>input {
    width: 300px;
    height: 40px;
    padding-left: 20px;
    display: block;
    margin-bottom: 30px;
    margin-right: auto;
    margin-left: auto;
    border: 1px solid #373e45;
}

.update>button {
    width: 320px;
    height: 40px;
    border: 1px solid #373e45;
    background-color: #373e45;
    color: #fff;
    cursor: pointer;
}
</style> 