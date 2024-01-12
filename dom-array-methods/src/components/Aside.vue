<template>
    <aside>
        <button @click="addUser">Add User 👱‍♂️</button>
        <button @click="doubleMoney">Double Money 💰</button>
        <button @click="showMillionaire">Show Only Millionaires 💵</button>
        <button @click="sort">Sort by Richest ↓</button>
        <button @click="totalWealth">Calculate entire Wealth 🧮</button>
    </aside>
</template>

<script setup>
const emit = defineEmits(['getUser', 'doubleMoney', 'showMillionaire', 'sortRichest', 'calcTotal'])

const addUser = () => {
    emit('getUser')
}

const doubleMoney = () => {
    emit('doubleMoney')
}

const showMillionaire = () => {
    emit('showMillionaire')
}

const sort = () => {
    emit('sortRichest')
}

const totalWealth = () => {
    emit('calcTotal')
}
</script>