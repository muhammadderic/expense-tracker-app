<script setup>
  import MainBalance from './components/MainBalance.vue';
  import MainHeader from './components/MainHeader.vue'
</script>

<template>
  <MainHeader/>  
  <div class="container">
    <MainBalance :total="100"/>
  </div>
</template>