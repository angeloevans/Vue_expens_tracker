<template>
  <!-- Header component, typically used for displaying the app title or header content -->
  <Header />

  <!-- Main container for all content -->
  <div class="container">
    <!-- Balance component displaying the total balance, passed as a prop -->
    <Balance :total="total"/>

    <!-- IncomeExpenses component displaying income and expenses, passed as props -->
    <IncomeExpenses :income="+income" :expenses="+expenses"/>

    <!-- TransactionList component displaying a list of transactions, and handling the deletion event -->
    <TransactionList :transactions="transactions" @transactionDeleted="handleTransactionDeleted" />

    <!-- AddTransaction component for adding new transactions, emitting an event when a transaction is submitted -->
    <AddTransaction @transactionSubmited="handleTransactionSubmited"/>
  </div>
</template>

<script setup>
  // Importing necessary components
  import Header from './components/Header.vue';
  import Balance from './components/Balance.vue';
  import IncomeExpenses from './components/IncomeExpenses.vue';
  import TransactionList from './components/TransactionList.vue';
  import AddTransaction from './components/AddTransaction.vue';

  // Importing toast notification for success/failure messages
  import { useToast } from 'vue-toastification';

  // Vue Composition API imports
  import { ref, computed, onMounted } from 'vue';

  // Creating a toast notification instance
  const toast = useToast();

  // Reactive variable to store the list of transactions
  const transactions = ref([]);

  // Load transactions from localStorage when the component is mounted
  onMounted(() => {
    const savedTransactions = JSON.parse(localStorage.getItem('transactions'));
    if (savedTransactions) {
      transactions.value = savedTransactions;
    }
  });

  // Computed property for calculating total balance
  const total = computed(() => {
    return transactions.value.reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0);
  });

  // Computed property for calculating total income
  const income = computed(() => {
    return transactions.value
      .filter((transaction) => transaction.amount > 0)
      .reduce((acc, transaction) => {
        return acc + transaction.amount;
      }, 0).toFixed(2);
  });

  // Computed property for calculating total expenses
  const expenses = computed(() => {
    return transactions.value
      .filter((transaction) => transaction.amount < 0)
      .reduce((acc, transaction) => {
        return acc + transaction.amount;
      }, 0).toFixed(2);
  });

  // Function to handle the submission of a new transaction
  const handleTransactionSubmited = (transactionData) => {
    // Add the new transaction to the list
    transactions.value.push({
      id: generateUniqueId(),
      text: transactionData.text,
      amount: transactionData.amount,
    });

    // Save the updated transactions to localStorage
    saveTransactionToLocalStorage();
    // Show a success toast message
    toast.success('Transaction Added');
  };

  // Function to generate a unique ID for new transactions
  const generateUniqueId = () => {
    return Math.floor(Math.random() * 1000000);
  };

  // Function to handle the deletion of a transaction
  const handleTransactionDeleted = (id) => {
    // Filter out the transaction that is being deleted
    transactions.value = transactions.value.filter((transaction) => transaction.id !== id);
    // Save the updated transactions to localStorage
    saveTransactionToLocalStorage();
    // Show a success toast message
    toast.success('Transaction Deleted!');
  };

  // Function to save the transactions list to localStorage
  const saveTransactionToLocalStorage = () => {
    localStorage.setItem('transactions', JSON.stringify(transactions.value));
  };
</script>
