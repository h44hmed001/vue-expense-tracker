<template>
  <h3>Add new transaction</h3>
  <form @submit.prevent="handleSubmit" id="form">
    <div class="form-control">
      <label for="text">Text</label>
      <input v-model="text" type="text" id="text" placeholder="Enter text..." />
    </div>
    <div class="form-control">
      <label for="amount"
        >Amount <br />
        (negative - expense, positive - income)</label
      >
      <input
        v-model="amount"
        type="number"
        id="amount"
        placeholder="Enter amount..."
      />
    </div>
    <button class="btn">Add transaction</button>
  </form>
</template>
<script setup>
import { ref } from "vue";
const amount = ref("");
const text = ref("");
const emit = defineEmits(["transactionAdded"]);
const handleSubmit = () => {
  const transactionData = {
    amount: amount.value,
    text: text.value,
  };
  amount.value = "";
  text.value = "";

  emit("transactionAdded", transactionData);
};
</script>
