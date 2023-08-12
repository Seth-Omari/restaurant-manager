<template>
    <Header />
    <h1>Hello {{ name }}, welcome on home page</h1>


    <table border="1">
        <tr>
            <td>ID</td>
            <td>NAME</td>
            <td>CONTACT</td>
            <td>ADDRESS</td>
            <td>ACTIONS</td>
        </tr>
        <tr v-for="item in restaurant" :key="item.id">
            <td>{{ item.id }}</td>
            <td>{{ item.name }}</td>
            <td>{{ item.contact }}</td>
            <td>{{ item.address }}</td>
            <td><router-link :to="'/update/' + item.id">Update</router-link>
                <button v-on:click="deleteRestaurant(item.id)">Delete</button>
            </td>

        </tr>
    </table>
</template>

<script>
import Header from './Header.vue'
import axios from 'axios'
export default {
    name: 'HomePage',
    data() {
        return {
            name: '',
            restaurant: []
        }
    },
    components: {
        Header
    },
    methods: {
        async deleteRestaurant(id) {
            console.warn(id)
            let result = await axios.delete("http://localhost:3000/restaurants/"+id)

            if (result.status == 200){
                this.loadData()
            }

        },

        async loadData() {
            let user = localStorage.getItem('user-info')
            this.name = JSON.parse(user).name
            if (!user) {
                this.$router.push({ name: 'SignUp' })
            }

            let result = await axios.get("http://localhost:3000/restaurants")

            console.warn(result)

            this.restaurant = result.data
        }
    },
    async mounted() {
       this.loadData()
    }
}
</script>

<style>
td {
    width: 200 px;
    height: 40 px;
}
</style>