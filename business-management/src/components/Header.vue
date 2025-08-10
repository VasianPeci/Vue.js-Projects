<template>
    <nav>
        <router-link :to="{name: 'Home'}">Home</router-link>
        <router-link :to="{name: 'Add'}">Add Business</router-link>
        <a @click="logout()">Log Out</a>
    </nav>
</template>

<script setup>

import { useRouter } from 'vue-router';

const router = useRouter();

function logout() {
    localStorage.clear();
    router.push({name: "LogIn"});
}

</script>

<style scoped>

nav {
    background-color: rgb(0, 0, 0);
    overflow: hidden;
    display: flex;
    justify-content: flex-start;
    align-items: center;
}

nav a {
    color: white;
    text-align: center;
    padding: 10px 14px;
    text-decoration: none;
    font-size: 20px;
    margin-right: 20px;
}

nav a:hover {
    background-color: white;
    color: #000;
    cursor: pointer;
}

</style>