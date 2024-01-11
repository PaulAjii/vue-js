<template>
  <main class="w-5/6 mx-auto sm:w-4/6 sm:flex sm:justify-between">
    <div class="flex flex-col pb-2">
      <span class="mb-2 border-b-2">Add Task</span>
      <AddTaskForm @task-submitted="taskSubmit" />
    </div>

    <div class="w-full sm:w-3/6">
      <h2 class="border-b-2 mb-4">
        Tasks
      </h2>
  
      <ul v-if="tasks.length > 0" class="list-none mb-8" v-for="task in tasks" :key="task.id">
        <li class="flex gap-2 justify-between align-center pr-4 pl-2 py-2 mb-1 border-2 rounded-lg cursor-pointer" @dblclick="handleUpdate(task)" title="Double Click to toggle complete.">
          <div class="flex gap-3 align-center">
            <input type="checkbox" name="isPending" id="isPending" v-model="task.isCompleted" @click="handleUpdate(task)" class="mr-2 w-3">
            <span class="opacity-80 text-base">{{ task.name }}</span>
          </div>
          <button class="align-self-end text-red-600 cursor-pointer text-lg" @click="handleDelete(task.id)" title="Click to delete.">x</button>
        </li>
      </ul>
  
      <p v-else class="mb-8">No task has been created. Create a task.</p>
    </div>
  </main>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import AddTaskForm from '@/components/AddTaskForm.vue'

const tasks = ref([])

onMounted(() => {
  const savedTask = JSON.parse(localStorage.getItem("tasks"))

  if(savedTask) {
    tasks.value = savedTask
  }
})

const saveToLocalStorage = () => {
  localStorage.setItem("tasks", JSON.stringify(tasks.value))
}

const taskSubmit = (taskInfo) => {
  tasks.value.push({
        id: Math.floor(Math.random() * 1000000),
        name: taskInfo.name,
        isCompleted: false
  })

  saveToLocalStorage()
}

const handleDelete = (id) => {
  tasks.value = tasks.value.filter((task) => {
    return task.id !== id
  })

  saveToLocalStorage()
}

const handleUpdate = (task) => {
  task.isCompleted = !task.isCompleted

  saveToLocalStorage()
}
</script>
