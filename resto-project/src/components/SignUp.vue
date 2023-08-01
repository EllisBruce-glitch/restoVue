<template>
    <img class="logo" alt="Vue logo" src="../assets/resto-logo.png">
    <h1>Sign Up</h1>
    <div class="register">
        <input type="text" v-model="name" placeholder="Enter Name" />
        <input type="text" v-model="email" placeholder="Enter Email" />
        <input type="password" v-model="password" placeholder="Enter Password" />
        <button v-on:click="signUp">Sign Up</button>
        <p>
            <a href="/login"> Login</a>
        </p>
    </div>
</template>

<script>

import axios from 'axios'

export default {
    name: 'SignUp',
    data() {
        return {
            name: '',
            email: '',
            password: ''
        }
    },
    methods: {
        async signUp() {
            let result = await axios.post("http://localhost:3000/users", {
                email: this.email,
                name: this.name,
                password: this.password
            });

            console.warn(result);
            if (result.status == 201) {
                alert("sign up successfully");
                this.$router.push({ name: 'HomePage' })
                localStorage.setItem("user-info", JSON.stringify(result.data))
            }
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

.register>input {
    width: 300px;
    height: 40px;
    padding-left: 20px;
    display: block;
    margin-bottom: 30px;
    margin-right: auto;
    margin-left: auto;
    border: 1px solid #373e45;
}

.register>button {
    width: 320px;
    height: 40px;
    border: 1px solid #373e45;
    background-color: #373e45;
    color: #fff;
    cursor: pointer;
}
</style>

