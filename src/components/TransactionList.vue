<script setup>
  import { ref, computed, defineProps, defineEmits } from 'vue';

const props = defineProps(['transactions']);
const emit = defineEmits(['delete-transaction']);
const filterType = ref('All');

const filteredTransactions = computed(() => {
  if (filterType.value === 'All') return props.transactions;
  return props.transactions.filter(t => t.type === filterType.value);
});
</script>

<template>
  <div>
    <div class="mb-4">
      <button @click="filterType = 'All'" class="btn btn-outline-info me-2 px-5">All</button>
      <button @click="filterType = 'Income'" class="btn btn-outline-success me-2">Income</button>
      <button @click="filterType = 'Expense'" class="btn btn-outline-danger">Expense</button>
    </div>
    <table class="table table-bordered table-hover">
      <thead>
        <tr>
          <th>Title</th>
          <th>Amount</th>
          <th>Type</th>
          <th>Action</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(transaction, index) in filteredTransactions" :key="index">
          <td>{{ transaction.title }}</td>
          <td  :class="{ 
                'text-success': transaction.type === 'Income', 
                'text-danger': transaction.type === 'Expense', 
                'fw-bold': transaction.type === 'Expense' && transaction.amount >= 500}">   
            ${{ transaction.amount }}
          </td>
          <td class="text-uppercase">{{ transaction.type }}</td>
          <td>
            <button @click="$emit('delete-transaction', index)" class="btn btn-danger btn-sm">Delete</button>
          </td>
        </tr>
        <tr v-if="filteredTransactions.length === 0">
          <td colspan="4" class="text-center">No transactions recorded yet.</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<style scoped>

</style>