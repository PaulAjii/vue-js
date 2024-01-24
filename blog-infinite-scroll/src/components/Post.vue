<template>
  <div v-for="post in posts" :key="post.id" class="post">
    <div class="number">{{ post.id }}</div>
    <div class="post-info">
      <h2 class="post-title">{{ post.title }}</h2>
      <p class="post-body">{{ post.body }}</p>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
    posts: {
        type: Array,
        required: true
    }
})
</script>