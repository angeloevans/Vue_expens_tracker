<template>
  <!-- Container for both income and expense sections -->
  <div class="inc-exp-container">
    
    <!-- Income Section -->
    <div>
      <h4>Income</h4>
      <!-- Display income, formatted as currency -->
      <p id="money-plus" class="money plus">€{{ income }}</p>
    </div>

    <!-- Expense Section -->
    <div>
      <h4>Expense</h4>
      <!-- Display expenses, formatted as currency -->
      <p id="money-minus" class="money minus">€{{ expenses }}</p>
    </div>
  </div>
</template>

<script setup>
  // Import `defineProps` to define the props the component will accept
  import { defineProps } from 'vue';

  // Define the props that this component expects
  const props = defineProps({
    // Income prop: should be a number and is required
    income: {
      type: Number,
      required: true,
    },
    
    // Expense prop: should be a number and is required
    expenses: {
      type: Number,
      required: true,
    }
  })
</script>
