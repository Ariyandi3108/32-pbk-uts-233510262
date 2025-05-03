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
  <div>
    <input type="text" v-model="newTask" @keyup.enter="addTask">
    <button @click="addTask">Add Task</button>
    <select v-model="filter">
      <option value="all">All</option>
      <option value="active">Active</option>
      <option value="completed">Completed</option>
    </select>

    <ul>
      <li v-for="task in filteredTasks" :key="task.id">
        <input type="checkbox" v-model="task.completed" @change="toggleTask(task)">
        {{ task.title }}
        <button @click="removeTask(task)">Remove</button>
      </li>
    </ul>
  </div>

</template>

<style scoped></style>
