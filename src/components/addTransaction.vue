<script setup>
  import { ref, defineEmits } from 'vue';

const emit = defineEmits(['add-transaction']);
const title = ref('');
const amount = ref(0);
const type = ref('Income');

const handleSubmit = () => {
  if (amount.value <= 0) return alert('Amount must be greater than zero.');
  const transaction = { title: title.value, amount: amount.value, type: type.value };
  emit('add-transaction', transaction);
  title.value = '';
  amount.value = 0;
  type.value = 'Income';
};
</script>

<template>
  <form @submit.prevent="handleSubmit" class="mb-4">
    <div class="mb-2 d-flex">
      <input v-model="title" type="text" class="form-control me-2" placeholder="Title" required />
      <input v-model.number="amount" type="number" class="form-control me-2" placeholder="Amount" required min="1" />
      <select v-model="type" class="form-select me-2">
        <option value="Income">Income</option>
        <option value="Expense">Expense</option>
      </select>
      <button type="submit" class="btn btn-primary w-100">Add</button>
    </div>
  </form>
</template>

<style scoped>
  
</style>