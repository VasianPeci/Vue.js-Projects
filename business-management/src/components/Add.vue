<template>
    <Header></Header>
    <h1>Add a Business</h1>
    <form>
        <input type="text" placeholder="Enter Name" name="name" v-model="business.name">
        <input type="text" placeholder="Enter Address" name="address" v-model="business.address">
        <input type="text" placeholder="Enter Contact" name="contact" v-model="business.contact">
        <button type="button" @click="addBusiness()">Add New Business</button>
    </form>
</template>

<script setup>

import axios from 'axios';
import { reactive, onMounted } from 'vue';
import Header from './Header.vue';
import { useRouter } from 'vue-router';

const router = useRouter();

const business = reactive({
    name: "",
    address: "",
    contact: ""
});

onMounted(() => {
    const user = localStorage.getItem('user-info');
    if (!user) {
        router.push({ name: "SignUp" });
    }
})

async function addBusiness() {
    let result = await axios.post("http://localhost:3000/businesses", business);

    if(result.status === 201) {
        alert("Successfully added the business!");
        router.push({name: "Home"});
    } else {
        alert("There was a problem in adding the business. Try again!");
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