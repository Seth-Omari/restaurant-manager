<template>
  
<router-view/>
</template>
import router from './routers';

<script>

//import SignUp from './components/SignUp.vue'
export default {
    name: "App"
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
 
}

body {

padding: 0;
margin: 0;
}

.logo {
    width: 100px
}

.register input, .login input, .add input{
    width: 300px;
    height: 40px;
    display: block;
    padding-left: 20 px;
    margin-right: auto;
    margin-bottom: 30px;
    margin-left: auto;
    border: 1px solid skyblue;
}

.register button, .login button, .add button{

    width: 320px;
    height: 40px;
    border: 1px solid skyblue;
    background: skyblue;
    color: #fff;
    cursor: pointer;
}
</style>
