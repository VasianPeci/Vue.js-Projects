<template>
    <Header></Header>
    <h1>Hello {{ name }}, Welcome to HomePage</h1>
    <table border="1">
        <tr class="first">
            <td>ID</td>
            <td>Name</td>
            <td>Address</td>
            <td>Contact</td>
            <td>Actions</td>
        </tr>
        <tr v-for="b in businesses" :key="b.id">
            <td>{{ b.id }}</td>
            <td>{{ b.name }}</td>
            <td>{{ b.address }}</td>
            <td>{{ b.contact }}</td>
            <td>
                <router-link class="active" :to="'/update/' + b.id">Update</router-link>
                <button @click="deleteBusiness(b.id)">Delete</button>
            </td>
        </tr>
    </table>
</template>

<script setup>

import axios from 'axios';
import { ref, onMounted } from 'vue';
import { useRouter } from 'vue-router';
import Header from './Header.vue';

const router = useRouter();
const name = ref('');
const businesses = ref([]);

onMounted(() => {
    loadData();
});

function loadData() {
    const user = localStorage.getItem('user-info');
    if (!user) {
        router.push({ name: "SignUp" });
    } else {
        name.value = JSON.parse(user).name;
    }

    getBusinesses();
}

async function getBusinesses() {
    let result = await axios.get("http://localhost:3000/businesses");
    businesses.value = result.data;
}

async function deleteBusiness(id) {
    let result = await axios.delete(`http://localhost:3000/businesses/${id}`);

    if(result.status === 200) {
        getBusinesses();
        router.push({name: "Home"});
    } else {
        alert("Not deleted. Try again!");
    }
}

</script>

<style scoped>

h1 {
    text-align: center;
}

table {
    margin: 0 auto;
}

td {
    text-align: center;
    width: 160px;
    height: 40px;
}

.first {
    background-color: black;
    color: white;
}

table button {
    margin-left: 5px;
    background-color: red;
    color: black;
    cursor: pointer;
    border-radius: 10%;
}

.active {
    text-decoration: none;
}

.active:hover {
    color: red;
}

</style>