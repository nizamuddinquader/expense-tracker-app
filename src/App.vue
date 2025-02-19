<script setup>
import { ref, onMounted } from 'vue';
import AddTransaction from './components/addTransaction.vue'
import TransactionList from './components/TransactionList.vue';

const transactions = ref([]);

onMounted(() => {
  const savedTransactions = localStorage.getItem('transactions');
  if (savedTransactions) {
    transactions.value = JSON.parse(savedTransactions);
  }
});

const addTransaction = (transaction) => {
  transactions.value.push(transaction);
  localStorage.setItem('transactions', JSON.stringify(transactions.value));
};

const deleteTransaction = (index) => {
  transactions.value.splice(index, 1);
  localStorage.setItem('transactions', JSON.stringify(transactions.value));
};
</script>

<template>
  <div class="container mt-5">
    <h1 class="text-center mb-5">Expense Tracker</h1>
    <Add-transaction @add-transaction="addTransaction"/>
    <Transaction-list :transactions="transactions" @delete-transaction="deleteTransaction"/>
  </div>
</template>

<style scoped>

</style>
