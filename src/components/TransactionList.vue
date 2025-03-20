<template>
  <h3>History</h3>
  <ul id="list" class="list">
    <li v-for="transaction in transactions" :key="transaction.id" :class="transaction.amount < 0 ? 'minus' : 'plus'">
      {{ transaction.text }}<span>€{{ transaction.amount }}</span>
      <button @click="deleteTransaction(transaction.id)" class="delete-btn">x</button>
    </li>
  </ul>
</template>

<script setup>
  import { defineProps } from 'vue';

  // Emit custom events from the child component to its parent component
  const emit = defineEmits(['transactionDeleted']); 

  // Data (transactions) is passed down from a parent component to this child component.
  const props = defineProps({
    transactions: {
      type: Array,
      required: true
    },
  })

  // Function to delete a transaction and notify the parent via the custom event
  const deleteTransaction = (id) => {
    // Emit the event 'transactionDeleted' with the transaction id
    emit('transactionDeleted', id);  
  }
</script>
