<template>
  <h3>History</h3>
  <ul id="list" class="list">
    <li
      :key="transaction.id"
      :class="transaction.amount > 0 ? 'plus' : 'minus'"
      v-for="transaction in transactions"
    >
      {{ transaction.text }} <span>${{ transaction.amount }}</span
      ><button @click="handleDelete(transaction.id)" class="delete-btn">
        x
      </button>
    </li>
  </ul>
</template>

<script setup>
import { defineProps } from "vue";
const props = defineProps({
  transactions: {
    type: Array,
    required: true,
  },
});
const emit = defineEmits(["transactionDeleted"]);
const handleDelete = (id) => {
  emit("transactionDeleted", id);
};
</script>
