<template>
    <main id="main">
        <h2><strong>Person</strong> Wealth</h2>

        <div v-for="person in people" class="person" :key="person.id">
            <strong>{{ person.name }}</strong>
            {{ formatMoney(parseInt(person.money)) }}
        </div>

        <h3 v-show="total">Total Wealth: <strong>{{ formatMoney(total) }}</strong></h3>
    </main>
</template>

<script setup>
const props = defineProps({
    people: {
        type: Array,
        required: true
    },

    total: {
        type: Number,
        required: true
    }
})

const formatMoney = (num) => {
    return '$' + num.toFixed(2).replace(/\d(?=(\d{3})+\.)/g, '$&,')
}
</script>