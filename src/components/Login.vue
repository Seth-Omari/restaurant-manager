<template>
    <img class="logo" src="../assets/restauranticon.png" />
    <h1>Login</h1>

    <div class="login">
        <input type="text" v-model="email" placeholder="Enter Email" />
        <input type="text" v-model="password" placeholder="Enter Password" />
        <button v-on:click="login">Login</button>
    </div>

    <p>
        <router-link to="/sign-up">
            Sign Up
        </router-link>
    </p>
</template>

<script>

import axios from 'axios';
export default {

    name: 'LoginPage',
    data() {
        return {
            email: '',
            password: ''
        }
    },
    methods: {
        async login() {
            //console.warn(this.email, this.password)

            let result = await axios.get(`http://localhost:3000/users?email=${this.email}&password=${this.password}`)

           // console.warn(result)

            if (result.status == 200 && result.data.length > 0) {
                //alert("Sign-up done")
                localStorage.setItem("user-info", JSON.stringify(result.data[0]));
                this.$router.push({ name: "Home" });
            }
        }
    },
    mounted() {
        let user = localStorage.getItem("user-info");
        if (user) {
            this.$router.push({ name: "Home" });
        }
    }
}


</script>