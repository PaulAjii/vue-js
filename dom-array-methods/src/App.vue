<template>
  <h1>DOM Array Methods</h1>
  <div class="container">
    <Aside @getUser="getRandomUser" @doubleMoney="handleDoubleMoney" @showMillionaire="handleShowMillionaire"
      @sortRichest="handleSortRichest" @calcTotal="handleCalcTotal" />
    <Home :people="people" :total="+total" />
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import Aside from './components/Aside.vue'
import Home from './components/Home.vue'

onMounted(() => {
  getRandomUser()
  getRandomUser()
  getRandomUser()
})

const fetchRandomNumber = () => {
  return Math.floor(Math.random() * 1000000)
}

const people = ref([])
const total = ref('')

const getRandomUser = async () => {
  try {
    const res = await fetch('https://randomuser.me/api')
    const data = await res.json()
    const user = data.results[0]

    const newUser = {
      id: fetchRandomNumber(),
      name: user.name.first + " " + user.name.last,
      money: fetchRandomNumber()
    }
    people.value.push(newUser)
    total.value = ''
  } catch (err) {
    console.log(err.message)
  }
}

const handleDoubleMoney = () => {
  people.value = people.value.map(user => {
    return { ...user, money: user.money * 2 }
  })
  total.value = ''
}

const handleShowMillionaire = () => {
  people.value = people.value.filter(person => person.money > 1000000)
  total.value = ''
}

const handleSortRichest = () => {
  people.value = people.value.sort((a, b) => b.money - a.money)

  total.value = ''
}

const handleCalcTotal = () => {
  total.value = people.value.reduce((acc, person) => acc += person.money, 0)
}
</script>