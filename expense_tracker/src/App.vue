<template>
  <Header></Header>
  <div class="container">
    <Balance :total="+total"></Balance>
    <IncomeExpenses :income="+income" :expenses="+expenses"></IncomeExpenses>
    <TransactionList :transactions="transactions" @transaction-deleted="handleTransactionDeleted"></TransactionList>
    <AddTransaction @transaction-submitted="handleTransactionSubmitted"></AddTransaction>
  </div>
</template>

<script setup>

import Header from './components/Header.vue';
import Balance from './components/Balance.vue';
import IncomeExpenses from './components/IncomeExpenses.vue';
import TransactionList from './components/TransactionList.vue';
import AddTransaction from './components/AddTransaction.vue';

import { useToast } from 'vue-toastification';
import {ref, computed, onMounted} from 'vue';

const toast = useToast();
const transactions = ref([]);

// Get Total
const total = computed(() => {
  return transactions.value.reduce((acc, transaction) => acc + transaction.amount, 0).toFixed(2);
});

// Get Income
const income = computed(() => {
  return transactions.value.filter(transaction => transaction.amount > 0).reduce((acc, transaction) => acc + transaction.amount, 0).toFixed(2);
});

// Get Expenses
const expenses = computed(() => {
  return transactions.value.filter(transaction => transaction.amount < 0).reduce((acc, transaction) => acc + transaction.amount, 0).toFixed(2);
});

// Add Transaction
function handleTransactionSubmitted(transactionData) {
  transactions.value.push({
    id: generateUniqueID(),
    text: transactionData.text,
    amount: transactionData.amount,
  });
  saveTransactionsToLocalStorage();
  toast.success("Transaction added");
}

// Generate a Unique ID
function generateUniqueID() {
  return Math.floor(Math.random() * 1000000);
}

// Delete Transaction
function handleTransactionDeleted(id) {
  transactions.value = transactions.value.filter(transactions => transactions.id !== id);
  saveTransactionsToLocalStorage();
  toast.success("Transaction deleted");
}

// Save Transactions to Local Storage
function saveTransactionsToLocalStorage() {
  localStorage.setItem("transactions", JSON.stringify(transactions.value));
}

onMounted(() => {
  const savedTransactions = JSON.parse(localStorage.getItem("transactions"));

  if(savedTransactions) {
    transactions.value = savedTransactions;
  }
});

</script>