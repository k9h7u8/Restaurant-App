<template>
<Header />
<h1>Hello, Welcome On Home Page</h1>
</template>

<script>
import Header from './HeaderPage.vue'
export default {
    name: "HomePage",
    components: {
        Header
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

</style>
