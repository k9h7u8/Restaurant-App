<template>
<Header />
<h1>Hello {{ name }}, Welcome On Home Page</h1>
<table border="1">
    <tr>
        <td>Id</td>
        <td>Name</td>
        <td>Address</td>
        <td>Contact</td>
        <td>Actions</td>
    </tr>
    <tr v-for="item in restaurants" :key="item.id">
        <td>{{item.id}}</td>
        <td>{{item.name}}</td>
        <td>{{item.address}}</td>
        <td>{{item.contact}}</td>
        <td>
            <router-link :to="'/update/' +item.id">Update</router-link>
            <button type="button" v-on:click="deleteRestaurant(item.id)">Delete </button>
        </td>
    </tr>
</table>
</template>

<script>
import axios from 'axios';
import Header from './HeaderPage.vue'
export default {
    name: "HomePage",
    components: {
        Header
    },
    data() {
        return {
            name: '',
            restaurants: []
        }
    },
    methods: {
        async deleteRestaurant(id) {
            let result = await axios.delete("http://localhost:3000/restaurant/" + id);
            if (result.status == 200) {
                this.loadData();
            }
        },
        async loadData() {
            let user = localStorage.getItem('user-info');
            this.name = JSON.parse(user).name
            if (!user) {
                this.$router.push({
                    name: "SignUp"
                })
            }
            let result = await axios.get("http://localhost:3000/restaurant");
            console.log(result);
            this.restaurants = result.data;
        }
    },
    mounted() {
        this.loadData();
    }
}
</script>

<style>
td {
    width: 160px;
    height: 40px;
}
</style>
