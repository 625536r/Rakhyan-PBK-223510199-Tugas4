<template>
  <div class="app">
    <header>
      <h1>Pencatatan Pembelanjaan</h1>
    </header>
    <expense-form @add-expense="addExpense"></expense-form>
    <expense-list :expenses="expenses">
      <expense-item-slot></expense-item-slot>
    </expense-list>
    <div class="totals">
      <h2>Total Pengeluaran: {{ totalExpense }}</h2>
    </div>
  </div>
</template>

<script>
import ExpenseForm from './components/ExpenseForm.vue';
import ExpenseList from './components/ExpenseList.vue';
import ExpenseItemSlot from './components/ExpenseItemSlot.vue';

export default {
  name: 'App',
  components: {
    ExpenseForm,
    ExpenseList,
    ExpenseItemSlot
  },
  data() {
    return {
      expenses: []
    };
  },
  computed: {
    totalExpense() {
      return this.expenses.reduce((total, expense) => total + expense.total, 0);
    }
  },
  methods: {
    addExpense(expense) {
      this.expenses.push(expense);
    }
  }
}
</script>

<style scoped>
.app {
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
  font-family: 'Arial', sans-serif;
}

header {
  background-color: #2c3e50;
  color: white;
  padding: 20px;
  text-align: center;
}

form {
  margin-bottom: 20px;
}

button {
  background-color: #3498db;
  color: white;
  border: none;
  padding: 10px 20px;
  cursor: pointer;
}

button:hover {
  background-color: #2980b9;
}

.totals {
  margin-top: 20px;
  border-top: 2px solid #2c3e50;
  padding-top: 10px;
}

h2 {
  margin-bottom: 10px;
}

h1 {
  font-size: 28px;
  margin-bottom: 20px;
}

.expense-item {
  border-bottom: 1px solid #ccc;
  padding: 10px 0;
  display: flex;
  justify-content: space-between;
}

.expense-item:last-child {
  border-bottom: none;
}

.expense-item .name {
  font-weight: bold;
}

.expense-item .amount {
  color: #e74c3c;
}

.expense-item .date {
  color: #95a5a6;
}

.expense-form input[type="text"],
.expense-form input[type="number"] {
  width: 100%;
  padding: 8px;
  margin-bottom: 10px;
}

.expense-form button {
  width: 100%;
}

.expense-form button[type="submit"] {
  background-color: #2ecc71;
}

.expense-form button[type="submit"]:hover {
  background-color: #27ae60;
}
</style>
