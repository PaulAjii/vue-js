<template>
  <Header />

  <div class="container">
    <Balance :total="+total" />
    <IncomeExpenses :income="+income" :expenses="+expenses" />
    <TransactionList :transactions="transactions" @transactionDeleted="handleDelete" />
    <AddTransaction @transactionSubmitted="handleTransaction" />
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from "vue"
import { useToast } from "vue-toastification"

import AddTransaction from "./components/AddTransaction.vue";
import Balance from "./components/Balance.vue"
import Header from "./components/Header.vue"
import IncomeExpenses from "./components/IncomeExpenses.vue";
import TransactionList from "./components/TransactionList.vue";

const toast = useToast()

const transactions = ref([])

onMounted(() => {
  const savedTransaction = JSON.parse(localStorage.getItem("transactions"))

  if (savedTransaction) {
    transactions.value = savedTransaction
  }
})

const saveToLocalStorage = () => {
  localStorage.setItem("transactions", JSON.stringify(transactions.value))
}

const total = computed(() => {
  return transactions.value
    .reduce((acc, transaction) => {
      return acc + transaction.amount
    }, 0)
    .toFixed(2)
})

// get Expenses
const expenses = computed(() => {
  return transactions.value
    .filter((transaction) => {
      return transaction.amount < 0
    })
    .reduce((acc, transaction) => {
      return acc + transaction.amount
    }, 0)
    .toFixed(2)
})

// get Income
const income = computed(() => {
  return transactions.value
    .filter((transaction) => {
      return transaction.amount > 0
    })
    .reduce((acc, transaction) => {
      return acc + transaction.amount
    }, 0)
    .toFixed(2)
})

const handleTransaction = (transactionData) => {
  transactions.value.push({
    id: Math.floor(Math.random() * 1000000),
    text: transactionData.text,
    amount: transactionData.amount
  })

  saveToLocalStorage()

  toast.success("Transaction Completed!")
}

const handleDelete = (id) => {
  transactions.value = transactions.value.filter((transaction) => transaction.id !== id)

  saveToLocalStorage()

  toast.success("Transaction Deleted!")
}
</script>