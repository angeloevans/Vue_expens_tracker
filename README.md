# Vue Expense Tracker

![Vue.js](https://img.shields.io/badge/Vue-3-brightgreen)
![License](https://img.shields.io/badge/License-MIT-green.svg)

## Description

A simple **Expense Tracker** built with the **Vue.js** framework. 
<br>The application allows users to manage their finances by adding income and expense transactions, calculating balances, and displaying transaction history. All data is stored in **localStorage** to persist even after refreshing the page.

### Features
- **Add income and expense transactions** with descriptions and amounts.
- **Track balance**, income, and expenses in real-time.
- **Persistent data storage** using `localStorage`.
- **Transaction history** with the ability to delete individual transactions.
- **Responsive design** for mobile and desktop.

## Technologies Used
- **Vue.js** - Framework for building the user interface.
- **Vue Composition API** - Provides reactivity and lifecycle management.
- **localStorage** - Stores transaction data persistently across sessions.
- **Vue Toastification** - For showing success and error messages.

## How to Run

1. Clone the repository:
   ```bash
   git clone https://github.com/angeloevans/Vue_expens_tracker.git
   cd Vue_expens_tracker

## How to Run

1. Clone the repository:
   ```bash
   git clone https://github.com/angeloevans/Vue_expens_tracker.git
   cd Vue_expens_tracker
   ```
2. Install the dependencies:
    ```bash
    npm install 
    ```
3. Run the development server:
    ```bash
    npm run serve 
    ```
4. Open your browser and go to http://localhost:5173 to see the app in action.

### Project Structure

- **src/components/**: Contains Vue components:
  - `Balance.vue`: Displays the total balance.
  - `IncomeExpenses.vue`: Displays the total income and expenses.
  - `TransactionList.vue`: Shows all transactions and provides the option to delete them.
  - `AddTransaction.vue`: Provides a form to add new transactions.
  - `Header.vue`: Displays the header for the application.
  
- **src/App.vue**: The main component that aggregates all others.

- **localStorage**: Persists transactions between sessions.

### How It Works

- Transactions are added via the `AddTransaction.vue` form.
- The `Balance.vue` and `IncomeExpenses.vue` components use computed properties to calculate total balance, income, and expenses dynamically.
- Transaction history is displayed and managed in the `TransactionList.vue` component.
- Data is saved in the `localStorage` to maintain state even after page reloads.

### License
This project is licensed under the MIT License 
