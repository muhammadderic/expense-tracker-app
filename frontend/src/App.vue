<script setup>
  import IncomeExpenses from './components/IncomeExpenses.vue';
import MainBalance from './components/MainBalance.vue';
  import MainHeader from './components/MainHeader.vue'
</script>

<template>
  <MainHeader/>  
  <div class="container">
    <MainBalance :total="100"/>
    <IncomeExpenses :income="100.00" :expense="50.00"/>
  </div>
</template>