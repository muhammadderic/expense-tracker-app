<script setup>
import AddTransaction from './components/AddTransaction.vue';
import IncomeExpenses from './components/IncomeExpenses.vue';
import MainBalance from './components/MainBalance.vue';
import MainHeader from './components/MainHeader.vue'
import TransactionsList from './components/TransactionsList.vue';

import { ref, computed, onMounted } from 'vue';
import {useToast} from 'vue-toastification';

const transactions = ref([]);
const toast = useToast();

// Mounted transactions value from local storage
onMounted(() => {
  const savedTransactions = JSON.parse(localStorage.getItem("transactions"));

  if (savedTransactions) {
    transactions.value = savedTransactions;
  }
})

// Get total balance
const total = computed(() => {
  return transactions.value.reduce((total, transaction) => {
    return total + transaction.amount;
  }, 0);
})

// Get income
const income = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((total, transaction) => total + transaction.amount, 0)
    .toFixed(2);
})

// Get expense
const expense = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount < 0)
    .reduce((total, transaction) => total + transaction.amount, 0)
    .toFixed(2);
})

const handleTransactionsSubmitted = (transactionData) => {
  transactions.value.push({
    id: generateId(),
    text: transactionData.text,
    amount: transactionData.amount,
  })

  saveTransactionsToLocalStorage();

  toast.success("Transaction added successfully");
}

// Generate a random id
const generateId = () => {
  return Math.floor(Math.random() * 1000000)
};

// Save transactions to local storage
const saveTransactionsToLocalStorage = () => {
  localStorage.setItem("transactions", JSON.stringify(transactions.value));
};
</script>

<template>
  <MainHeader/>  
  <div class="container">
    <MainBalance :total="total"/>
    <IncomeExpenses :income="income" :expense="expense"/>
    <TransactionsList :transactions="transactions"/>
    <AddTransaction @transactionSubmitted="handleTransactionsSubmitted"/>
  </div>
</template>