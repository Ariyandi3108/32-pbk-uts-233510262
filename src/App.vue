<script setup>
import { ref } from 'vue'

const tasks = ref([
  {
    id: 1,
    title: 'Task 1',
    completed: false
  },
  {
    id: 2,
    title: 'Task 2',
    completed: true
  },
  {
    id: 3,
    title: 'Task 3',
    completed: false
  }
])

</script>

<template>
  <div>
    <ul>
      <li v-for="task in tasks" :key="task.id">
        {{  task.title }} - {{ task.completed ? 'Completed' : 'Not Completed' }}
      </li>
    </ul>
  </div>
 
</template>

<style scoped>

</style>
