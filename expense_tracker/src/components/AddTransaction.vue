<template>
    <h3>Add New Transaction</h3>
    <form id="form" @submit.prevent="onSubmit">
        <div class="form-control">
            <label for="text">Text</label>
            <input type="text" id="text" placeholder="Enter text..." v-model="text">
        </div>
        <div class="form-control">
            <label for="amount">Amount <br>(negative - expense, positive - income)</label>
            <input type="text" id="amount" placeholder="Enter amount..." v-model="amount">
        </div>
        <button class="btn">Add Transaction</button>
    </form>
</template>

<script setup>

import { useToast } from 'vue-toastification';
import {ref} from 'vue';

const toast = useToast();
const emit = defineEmits(['transactionSubmitted']);

const text = ref('');
const amount = ref('');

function onSubmit() {
    if(!text.value || !amount.value) {
        toast.error("Fields must not be empty!");
        return;
    }
    if(isNaN(amount.value)) {
        toast.error("Amount must be a number!");
        return;
    }

    const transactionData = {
        text: text.value,
        amount: parseFloat(amount.value),
    };

    emit('transactionSubmitted', transactionData);

    text.value = "";
    amount.value = "";
}

</script>