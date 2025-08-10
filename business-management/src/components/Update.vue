<template>
    <Header></Header>
    <h1>Update the Business Data</h1>
    <form>
        <input type="text" placeholder="Enter Name" name="name" v-model="business.name">
        <input type="text" placeholder="Enter Address" name="address" v-model="business.address">
        <input type="text" placeholder="Enter Contact" name="contact" v-model="business.contact">
        <button type="button" @click="updateBusiness()">Update Business</button>
    </form>
</template>

<script setup>

import axios from 'axios';
import { reactive, onMounted } from 'vue';
import Header from './Header.vue';
import { useRoute, useRouter } from 'vue-router';

const route = useRoute();
const router = useRouter();

const business = reactive({
    name: "",
    address: "",
    contact: ""
});

onMounted(() => {
    if(!localStorage.getItem('user-info')) {
        router.push({name: "SignUp"});
    }
})

async function updateBusiness() {
    let result = await axios.put(`http://localhost:3000/restaurants/${route.params.id}`, business);

    if(result.status === 200) {
        alert("Updated successfully!");
        router.push({name: "Home"});
    } else {
        alert("Update not done. Try again!");
    }
}

</script>

<style scoped>

h1 {
    margin-top: 40px;
    text-align: center;
}

form {
    height: 60vh;
    display: flex;
    flex-direction: column;
    justify-content: center;
}

form input {
    width: 300px;
    height: 40px;
    padding-left: 20px;
    display: block;
    margin: 0 auto;
    margin-bottom: 30px;
    border: 1px solid black;
}

form button {
    display: block;
    width: 320px;
    height: 40px;
    border: 1px solid black;
    background-color: black;
    color: white;
    cursor: pointer;
    margin: 0 auto;
}

form button:hover {
    background-color: white;
    color: black;
}

</style>