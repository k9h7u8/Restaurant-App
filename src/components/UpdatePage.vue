<template>
<Header />
<h1>Hello, Welcome On Update Restaurant Page</h1>
<form class="update">
    <input v-model="restaurant.name" type="text" placeholder="Enter Restaurant Name" name="name" />
    <input v-model="restaurant.address" type="text" placeholder="Enter Restaurant Address" name="address" />
    <input v-model="restaurant.contact" type="text" placeholder="Enter Restaurant Contact" name="contact" />
    <button type="button" v-on:click="updateRestaurant()">Update Restaurant</button>
</form>
</template>

<script>
import axios from 'axios';
import Header from './HeaderPage.vue'
export default {
    name: "UpdatePage",
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
        async updateRestaurant() {
            const result = await axios.put("http://localhost:3000/restaurant/" + this.$route.params.id, {
                name: this.restaurant.name,
                address: this.restaurant.address,
                contact: this.restaurant.contact
            })
            if (result.status == 200) {
                this.$router.push({
                    name: "HomePage"
                })
            }
        }
    },
    async mounted() {
        let user = localStorage.getItem('user-info');
        if (!user) {
            this.$router.push({
                name: "SignUp"
            })
        }
        const result = await axios.get("http://localhost:3000/restaurant/" + this.$route.params.id);
        this.restaurant = result.data;
    }
}
</script>

<style>
.update input {
    width: 300px;
    height: 40px;
    padding-left: 20px;
    display: block;
    margin-bottom: 30px;
    margin-left: auto;
    margin-right: auto;
    border: 1px solid skyblue;
}

.update button {
    width: 320px;
    height: 40px;
    border: 1px solid skyblue;
    color: white;
    background-color: skyblue;
    cursor: pointer;
}
</style>
