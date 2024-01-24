<template>
  <div ref="container">
    <h1>My Blog</h1>

    <div class="filter-container">
      <input type="text" class="filter" placeholder="Filter Posts..." v-model="filterText">
    </div>
    <Post :posts="filteredPosts" v-if="filteredPosts" />
    <Post :posts="posts" v-else-if="posts" />
    <p v-else>Loading...</p>
    <div class="loader" :class="isLoading ? 'show' : ''">
      <Circle />
    </div>
  </div>
  <!-- <div class="last"></div> -->
</template>

<script setup>
import Circle from './components/Circle.vue'
import Post from './components/Post.vue'

import { ref, onMounted, watch } from 'vue'

const filterText = ref('')
const posts = ref(null)
const filteredPosts = ref(null)
const isLoading = ref(false)
const container = ref(null)

const limit = 5
const page = ref(2)

// const showLoading = () => {
//   isLoading.value = !isLoading.value

//   console.log(isLoading.value)
  
//   setTimeout(() => {
//     page.value += page.value

//     setTimeout(() => {
//       const newPosts = getPosts()
//       // console.log(typeof newPosts)
//       // posts.value.push([...newPosts])
//       // newPosts.map((post) => posts.value.push(post))
//       // console.log(posts.value)
//       console.log(newPosts)
//       console.log(page)
//     }, 300)
//   }, 1000)
// }

const handleScroll = () => {
  // console.log(scrollY)
  // if (container.value.scrollHeight - container.value.scrollTop === container.value.clientHeight) {
  //   showLoading()
  // }

  const { scrollTop, scrollHeight, clientHeight } = document.documentElement

  if (scrollHeight - scrollTop === clientHeight) {
    showLoading()
  }
}

const getPosts = async () => {
  const res = await fetch(
    `https://jsonplaceholder.typicode.com/posts?_limit=${limit}&_page=${page}`
  )
  const data = await res.json()
  return data
}

onMounted(async () => {
  posts.value = await getPosts()
})

watch(filterText, (newValue) => {
  filteredPosts.value = posts.value.filter(post => {
    return post.title.toUpperCase().includes(newValue.toUpperCase()) || post.body.toUpperCase().includes(newValue.toUpperCase())
  })
})

window.addEventListener('scroll', handleScroll)
</script>