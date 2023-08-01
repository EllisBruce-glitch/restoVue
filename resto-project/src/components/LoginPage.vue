<template>
    <img class="logo" alt="Vue logo" src="../assets/resto-logo.png">
    <h1>Login</h1>
    <div class="login">
        <input type="text" v-model="email" placeholder="Enter Email" />
        <input type="password" v-model="password" placeholder="Enter Password" />
        <button v-on:click="login">Login</button>
        <p>
            <a href="/signup"> SignUp</a>
        </p>
    </div>
</template>


<script>

import axios from 'axios';

export default {
    name: 'LoginPage',
    data() {
        return {
            email: '',
            password: ''
        }
    },
    methods: {

        async login() {
            let result = await axios.get(
                `http://localhost:3000/users?email=${this.email}&password=${this.password}`
            )

            if (result.status == 200 && result.data.length > 0) {
                localStorage.setItem("user-info", JSON.stringify(result.data))
                this.$router.push({ name: 'HomePage' })
            }
            console.warn(result);
        }

    },
    mounted() {
        let user = localStorage.getItem('user-info');
        if (user) {
            this.$router.push({ name: 'HomePage' })
        }
    }
}
</script>

<style scoped>
.logo {
    width: 100px;
    height: 100px;
}

.login>input {
    width: 300px;
    height: 40px;
    padding-left: 20px;
    display: block;
    margin-bottom: 30px;
    margin-right: auto;
    margin-left: auto;
    border: 1px solid #373e45;
}

.login>button {
    width: 320px;
    height: 40px;
    border: 1px solid #373e45;
    background-color: #373e45;
    color: #fff;
    cursor: pointer;
}
</style>

