<template>
  <h3>History</h3>
  <ul id="list" class="list" v-if="transactions.length > 0">
    <li v-for="transaction in transactions" :key="transaction.id" :class="transaction.amount < 0 ? 'minus' : 'plus'">
      {{ transaction.text }}
      <span>${{ transaction.amount }}</span>
      <button class="delete-btn" @click="deleteTransaction(transaction.id)">x</button>
    </li>
  </ul>

  <p v-else>There are no previous transactions history.</p>
</template>

<script setup>
import { defineProps } from 'vue'

const emit = defineEmits(["transactionDeleted"])

const props = defineProps({
  transactions: {
    type: Array,
    required: true
  }
})

const deleteTransaction = (id) => {
  emit("transactionDeleted", id)
}
</script>