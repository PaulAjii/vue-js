<template>
  <div class="flex justify-center align-center w-5/6 mx-auto sm:w-4/6">
    <header class="w-full mt-4 border-b-2 border-teal-50 pb-3 mb-8">
      <h1 class="mb-3.5 text-xl">Task Manager</h1>

      <nav class="flex gap-4">
        <RouterLink class="text-blue-900 transition duration-500 ease hover:text-blue-950" to="/">Home</RouterLink>
        <RouterLink class="text-blue-900 transition duration-500 ease hover:text-blue-950" to="/about">About</RouterLink>
      </nav>
    </header>

  </div>

  <RouterView />
</template>

<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>