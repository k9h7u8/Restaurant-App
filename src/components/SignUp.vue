<template>
<img class="logo" src="../assets/logo.jpg" />
<h1>Sign Up</h1>
<div class="register">
    <input type="text" placeholder="Enter Name" v-model="name" />
    <input type="text" placeholder="Enter Email" v-model="email" />
    <input type="password" placeholder="Enter Password" v-model="password" />
    <button v-on:click="signUp()">Sign Up</button>
</div>
</template>

<script>
import axios from 'axios';
export default {
    name: "SignUp",
    data() {
        return {
            name: '',
            email: '',
            password: ''
        }
    },
    methods: {
        async signUp() {
            let result =  await axios.post("http://localhost:3000/users", {
                name: this.name,
                email: this.email,
                password: this.password
            })
            console.warn(result);
            if(result.status==201){
              localStorage.setItem("user-info", JSON.stringify(result.data));
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
};
</script>

<style>
.logo {
    height: 100px;
    width: 100px;
}

.register input {
    width: 300px;
    height: 40px;
    padding-left: 20px;
    display: block;
    margin-bottom: 30px;
    margin-left: auto;
    margin-right: auto;
    border: 1px solid skyblue;
}

.register button {
    width: 320px;
    height: 40px;
    border: 1px solid skyblue;
    color: white;
    background-color: skyblue;
    cursor: pointer;
}
</style>
