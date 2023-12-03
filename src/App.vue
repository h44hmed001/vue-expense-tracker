<template>
  <Header />
  <Balance :total="total" />
  <IncomeExpense :income="income" :expense="expense" />
  <TransactionList
    @transactionDeleted="handleTransactionDeletion"
    :transactions="transactions"
  />
  <AddTransaction @transactionAdded="handleTransactionAdded" />
</template>
<script setup>
import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";
import IncomeExpense from "./components/IncomeExpense.vue";
import TransactionList from "./components/TransactionList.vue";
import AddTransaction from "./components/AddTransaction.vue";
import { computed, ref } from "vue";
const transactions = ref([]);

const total = computed(() => {
  return transactions.value.reduce((acc, transaction) => {
    return acc + transaction.amount;
  }, 0);
});
const income = computed(() => {
  return transactions.value
    .filter((item) => {
      return item.amount > 0;
    })
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0);
});
const expense = computed(() => {
  return transactions.value
    .filter((item) => {
      return item.amount < 0;
    })
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0);
});
const handleTransactionAdded = (transactionData) => {
  transactions.value.push({
    id: generateUniqueId(),
    amount: transactionData.amount,
    text: transactionData.text,
  });
};

const generateUniqueId = () => {
  return Math.floor(Math.random() * 100000000);
};
const handleTransactionDeletion = (id) => {
  transactions.value = transactions.value.filter(
    (transaction) => transaction.id !== id
  );
};
</script>
