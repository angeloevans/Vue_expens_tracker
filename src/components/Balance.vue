<template>
    <!-- Display the total balance passed as a prop -->
    <h4 id="balance">Your Balance: €{{ total }}</h4>
  </template>
  
  <script setup>
  // Import `defineProps` to define the props the component will accept
  import { defineProps } from 'vue';
  
  // Define the props for this component
  const props = defineProps({
    total: {
      type: Number,  // The type of the prop should be a number
      required: true, // This prop is required to be passed from the parent component
    }
  });
  </script>
  