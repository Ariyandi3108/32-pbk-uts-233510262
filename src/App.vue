<script setup>
import { ref, computed } from 'vue'

const tasks = ref([])
const newTask = ref('')
const filter = ref('all')

const addTask = () => {
  if (newTask.value !== '') {
    tasks.value.push({
      id: Date.now(),
      title: newTask.value,
      completed: false
    })
  }
  newTask.value = ''
}

const removeTask = (task) => {
  tasks.value = tasks.value.filter(t => t.id !== task.id)
}

const toggleTask = (task) => {
  task.completed == !task.completed
}

const filteredTasks = computed(() => {
  if (filter.value === 'completed') {
    return tasks.value.filter(task => task.completed)
  } else if (filter.value === 'active') {
    return tasks.value.filter(task => !task.completed)
  } else {
    return tasks.value
  }
})

</script>

<template>
  <div class="min-h-screen bg-gradient-to-br from-gray-900 to-gray-800 text-white flex flex-col items-center justify-center overflow-hidden">
    <div class="w-full max-w-md px-4 md:px-6 py-6 bg-gray-950/60 rounded-xl shadow-xl border border-gray-700">
      <h1 class="text-2xl font-bold text-center mb-6 text-cyan-400">Task Manager</h1>

      <div class="flex gap-2 mb-4">
        <input
          type="text"
          v-model="newTask"
          @keyup.enter="addTask"
          placeholder="Enter new task..."
          class="flex-1 px-4 py-2 bg-gray-800 text-white rounded-lg focus:outline-none focus:ring-2 focus:ring-cyan-500 transition"
        />
        <button
          @click="addTask"
          class="bg-cyan-500 hover:bg-cyan-600 text-white px-4 py-2 rounded-lg transition"
        >
          Add
        </button>
      </div>

      <select
        v-model="filter"
        class="w-full mb-4 bg-gray-800 text-white py-2 px-3 rounded-lg border border-gray-700 focus:outline-none"
      >
        <option value="all">All</option>
        <option value="active">Active</option>
        <option value="completed">Completed</option>
      </select>

      <div class="max-h-[250px] md:h-80 lg:h-100 overflow-y-auto scrollbar-thin scrollbar-thumb-cyan-500 scrollbar-track-gray-700 rounded-lg">
        <ul class="space-y-3">
          <li
            v-for="task in filteredTasks"
            :key="task.id"
            class="flex justify-between items-center bg-gray-800 px-4 py-2 rounded-lg hover:bg-gray-700 transition"
          >
            <div class="flex items-center gap-2">
              <input type="checkbox" v-model="task.completed" @change="toggleTask(task)" class="accent-cyan-500 w-4 h-4" />
              <span :class="{ 'line-through text-gray-400': task.completed }">{{ task.title }}</span>
            </div>
            <button
              @click="removeTask(task)"
              class="text-red-400 hover:text-red-500 transition"
            >
              Delete
            </button>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<style scoped>
.scrollbar-thin {
  scrollbar-width: thin;
}
</style>

