<script setup>
  import IncomeExpenses from './components/IncomeExpenses.vue';
import MainBalance from './components/MainBalance.vue';
  import MainHeader from './components/MainHeader.vue'
import TransactionsList from './components/TransactionsList.vue';
</script>

<template>
  <MainHeader/>  
  <div class="container">
    <MainBalance :total="100"/>
    <IncomeExpenses :income="100.00" :expense="50.00"/>
    <TransactionsList :transactions="[
      { id: 1, text: 'Salary', amount: 500, },
      { id: 2, text: 'Book', amount: -10, },
      { id: 3, text: 'Camera', amount: -150 }
    ]"/>
  </div>
</template>