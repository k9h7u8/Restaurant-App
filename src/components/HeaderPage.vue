<template>
<div class="nav">
    <router-link to="/">Home</router-link>
    <router-link to="/add">Add Restaurant</router-link>
    <a href="#" v-on:click="logout()">Logout</a>
</div>
</template>

<script>
export default {
    name: 'HeaderPage',
    methods:{
        logout(){
            localStorage.clear();
            this.$router.push({name: "LoginPage"})
        }
    }
}
</script>

<style>
    .nav{
        background-color: #333;
        overflow: hidden;
    }
    .nav a{
        float: left;
        color: #f2f2f2;
        text-align: center;
        padding: 16px 14px;
        text-decoration: none;
        font-size: 16px;
        margin-right: 5px;
    }
    .nav a:hover{
        background-color: #ddd;
        color:#222
    }
</style>
