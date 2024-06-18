<template>
<img class="logo" src="../assets/logo.jpg" />
<h1>Login</h1>
<div class="login">
    <input type="text" placeholder="Enter Email" v-model="email" />
    <input type="password" placeholder="Enter Password" v-model="password" />
    <button v-on:click="login()">Login</button>
    <p>
        <router-link to="/sign-up">Sign Up</router-link>
    </p>
</div>
</template>

<script>
import axios from 'axios';
export default {
    name: "LoginPage",
    data() {
        return {
            email: '',
            password: ''
        }
    },
    methods: {
        async login() {
            let result =await axios.get(`http://localhost:3000/users?email=${this.email}&password=${this.password}`);

            if(result.status==200 && result.data.length >0){
              localStorage.setItem("user-info", JSON.stringify(result.data[0]));
              this.$router.push({name: "HomePage"})
            }
        }
    },
    mounted(){
      let user = localStorage.getItem('user-info');
      if(user){
        this.$router.push({name: "HomePage"})
      }
    }
}
</script>

<style>
.logo {
    height: 100px;
    width: 100px;
}

.login input {
    width: 300px;
    height: 40px;
    padding-left: 20px;
    display: block;
    margin-bottom: 30px;
    margin-left: auto;
    margin-right: auto;
    border: 1px solid skyblue;
}

.login button {
    width: 320px;
    height: 40px;
    border: 1px solid skyblue;
    color: white;
    background-color: skyblue;
    cursor: pointer;
}
</style>