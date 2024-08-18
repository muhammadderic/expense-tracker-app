<script setup>
const props = defineProps({
  transactions: {
    type: Array,
    required: true,
  },
});

const emit = defineEmits(["deleteTransaction"]);

const deleteTransaction = (id) => {
  emit("deleteTransaction", id);
}

</script>

<template>
  <h3>History</h3>
  <ul id="list" class="list">
    <li 
      v-for="transaction in props.transactions" 
      :key="transaction.id"
      :class="transaction.amount > 0 ? 'plus' : 'minus'"
    >
      {{ transaction.text }}
      <span>
        ${{ transaction.amount }}
      </span>
      <button 
        class="delete-btn"
        @click="deleteTransaction(transaction.id)"
      >
        x
      </button>
    </li>
  </ul>
</template>