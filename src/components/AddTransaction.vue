<template>
  <h3>Add new transaction</h3>
  <form id="form" @submit.prevent="onSubmit">
    <div class="form-control">
      <label for="text">Description</label>
      <input type="text" id="text" v-model="text" placeholder="Enter description..." />
    </div>
    <div class="form-control">
      <label for="amount">
        Amount <br />
        (negative - expense, positive - income)
      </label>
      <input type="text" id="amount" v-model="amount" placeholder="Enter amount..." />
    </div>
    <button class="btn">Add transaction</button>
  </form>
</template>

<script setup>
import { ref } from 'vue'; // Create a reactive variable that automatically tracks changes and updates the DOM when the value changes.
import { useToast } from 'vue-toastification'; // Use a toast notification library for displaying small pop-up messages.

const text = ref('');  // Reactive reference for transaction description (text).
const amount = ref('');  // Reactive reference for transaction amount (positive or negative).

// Define emits: custom event 'TransactionSubmited' to notify the parent component when a new transaction is added.
const emit = defineEmits(['TransactionSubmited']);  

const toast = useToast(); // Initialize the toast notification.

const onSubmit = () => {
  // Check if both text and amount fields are filled out
  if (!text.value || !amount.value) {
    // Display a toast error message if either field is empty
    toast.error('Both fields must be filled.');
    return;
  }

  // Create a transaction object to hold the data
  const transactionData = {
    text: text.value,   // Transaction description (text)
    amount: parseFloat(amount.value) // Parse the amount as a float (positive for income, negative for expense)
  };

  // Emit the custom event 'TransactionSubmited' to pass the transaction data to the parent component
  emit('TransactionSubmited', transactionData); 

  // Clear the form fields after submission
  text.value = '';
  amount.value = '';
};
</script>
