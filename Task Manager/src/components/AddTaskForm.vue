<template>
    <form class="w-full mx-auto mb-5" @submit.prevent="handleSubmit">
        <div class="flex gap-3 items-end">
            <label for="name">Task:</label>
            <div class="flex justify- items-end w-full border-b-2 px-2 pt-3 pb-2">
                <input type="text" v-model="name" placeholder="e.g. Go to the stores..." id="name" class="w-full border-0 outline-none text-sm" required>
                <button type="submit" class="bg-blue-500 px-4 py-1.5 rounded text-white text-sm">Submit</button>
            </div>
        </div>
    </form>
</template>

<script setup>
import { ref } from "vue"

const name = ref("")

const emit = defineEmits(["taskSubmitted"])

const handleSubmit = () => {
    if (!name.value) return

    const taskInfo = {
        name: name.value,
    }

    emit("taskSubmitted", taskInfo)

    name.value = ""
}
</script>