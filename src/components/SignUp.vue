<template>
    <img class="logo" src="../assets/restauranticon.png" />
    <h1>Sign Up</h1>

    <div class="register">
        <input type="text" v-model="name" placeholder="Enter name" />
        <input type="text" v-model="email" placeholder="Enter Email" />
        <input type="text" v-model="password" placeholder="Enter Password" />
        <button v-on:click="signUp">Sign Up</button>
    </div>

    <p>
        <router-link to="/login">
            Login
        </router-link>
    </p>
</template>

<script>

import axios from 'axios'

export default {
    name: "SignUp",
    data() {
        return {
            name: "",
            email: "",
            password: ""
        };
    },
    methods: {
        async signUp() {
            let result = await axios.post("http://localhost:3000/users", {
                name: this.name,
                email: this.email,
                password: this.password
            });
            console.warn(result);
            if (result.status == 201) {
                //alert("Sign-up done")
                localStorage.setItem("user-info", JSON.stringify(result.data));
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







