<template>
    <div class="nav">
        <a href="/">Home</a>
        <a href="/add">Add Restaurant</a>
        <a v-on:click="logout" href="#">Logout</a>
    </div>
</template>

<script>
export default {
    name: 'HeaderComponent',
    methods: {
        logout() {
            localStorage.clear();
            this.$router.push({
                name: 'LoginPage'
            })
            console.warn("logout")
        }
    }
}
</script>

<style>
.nav {
    background-color: #292c2f;
    overflow: hidden;
}

.nav a {
    float: left;
    color: #fff;
    padding: 14px;
    text-align: center;
    font-size: 17px;
    text-decoration: none;
    margin-right: 5px;
}


.nav a:hover {
    background-color: #ddd;
    color: #333;
}
</style>