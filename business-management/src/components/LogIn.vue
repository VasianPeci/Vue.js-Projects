<template>
    <img class="logo" src="../assets/logo.png" alt="Logo">
    <h1>Log In</h1>
    <div class="login">
        <input type="text" v-model="email" placeholder="Enter Email">
        <input type="password" v-model="password" placeholder="Enter Password">
        <button @click="login()">Log In</button>
        <p>
            <router-link :to="{name: 'SignUp'}">Sign Up</router-link>
        </p>
    </div>
</template>

<script setup>

import {ref} from 'vue';
import { useRouter } from 'vue-router';
import axios from 'axios';

const router = useRouter();
const email = ref('');
const password = ref('');

async function login() {
    let result = await axios.get(`http://localhost:3000/users?email=${email.value}&password=${password.value}`);
    if(result.status === 200 && result.data.length > 0) {
        localStorage.setItem('user-info', JSON.stringify(result.data[0]));
        router.push({name: "Home"});
    } else {
        alert("Could not login. Try again!");
    }
}

</script>

<style scoped>

.logo {
    display: block;
    width: 100px;
    margin: 0 auto;
}

h1 {
    text-align: center;
}

.login input {
    width: 300px;
    height: 40px;
    padding-left: 20px;
    display: block;
    margin: 0 auto;
    margin-bottom: 30px;
    border: 1px solid black;
}

.login button {
    display: block;
    width: 320px;
    height: 40px;
    border: 1px solid black;
    background-color: black;
    color: white;
    cursor: pointer;
    margin: 0 auto;
}

.register button:hover {
    background-color: white;
    color: black;
}

p {
    text-align: center;
}

</style>