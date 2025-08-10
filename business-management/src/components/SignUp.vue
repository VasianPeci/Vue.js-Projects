<template>
    <img class="logo" src="../assets/logo.png" />
    <h1>Sign Up</h1>
    <div class="register">
        <input type="text" v-model="name" placeholder="Enter Name">
        <input type="text" v-model="email" placeholder="Enter Email">
        <input type="password" v-model="password" placeholder="Enter Password">
        <button @click="signUp()">Sign Up</button>
        <p>
            <router-link :to="{name: 'LogIn'}">Log In</router-link>
        </p>
    </div>
</template>

<script setup>

import axios from 'axios';
import {ref, onMounted} from 'vue';
import { useRouter } from 'vue-router';

const name = ref("");
const email = ref("");
const password = ref("");
const router = useRouter();

async function signUp() {
    const obj = {
        name: name.value,
        email: email.value,
        password: password.value
    }
    let result = await axios.post("http://localhost:3000/users", obj);

    if(result.status === 201) {
        localStorage.setItem("user-info", JSON.stringify(result.data));
        router.push({name: "Home"});
    } else {
        alert("There was an error in signing up. Try again!");
    }
}

onMounted(() => {
    if(localStorage.getItem('user-info')) {
        router.push({name: "Home"});
    }
});

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

.register input {
    width: 300px;
    height: 40px;
    padding-left: 20px;
    display: block;
    margin: 0 auto;
    margin-bottom: 30px;
    border: 1px solid black;
}

.register button {
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