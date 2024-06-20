<template>
<Header />
<h1>Hello, Welcome On Add Restaurant Page</h1>
<form class="add">
    <input v-model="restaurant.name" type="text" placeholder="Enter Restaurant Name" name="name" />
    <input v-model="restaurant.address" type="text" placeholder="Enter Restaurant Address" name="address" />
    <input v-model="restaurant.contact" type="text" placeholder="Enter Restaurant Contact" name="contact" />
    <button type="button" v-on:click="addRestaurant()">Add New Restaurant</button>
</form>
</template>

<script>
import axios from 'axios';
import Header from './HeaderPage.vue'
export default {
    name: "AddPage",
    components: {
        Header
    },
    data() {
        return {
            restaurant: {
                name: '',
                address: '',
                contact: '',
            }
        }
    },
    methods: {
        async addRestaurant() {
            let result = await axios.post("http://localhost:3000/restaurant", {
                name: this.restaurant.name,
                address: this.restaurant.address,
                contact: this.restaurant.contact
            })
            this.restaurant.name = '';
            this.restaurant.address = '';
            this.restaurant.contact = '';
            console.log(result);
        }
    },

    mounted() {
        let user = localStorage.getItem('user-info');
        if (!user) {
            this.$router.push({
                name: "SignUp"
            })
        }
    }
}
</script>

<style>
.add input {
    width: 300px;
    height: 40px;
    padding-left: 20px;
    display: block;
    margin-bottom: 30px;
    margin-left: auto;
    margin-right: auto;
    border: 1px solid skyblue;
}

.add button {
    width: 320px;
    height: 40px;
    border: 1px solid skyblue;
    color: white;
    background-color: skyblue;
    cursor: pointer;
}
</style>
