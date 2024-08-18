<template>
  <h1>Hello {{ name }}</h1>
  <form action="" @submit.prevent="addTask">
    <input type="text" placeholder="Créer une nouvelle tâche" v-model="taskName">
    <button>Ajouter</button>
    <p v-show="taskNumber <= 0">Il n'y a aucune tâches en cours...</p>
  </form>
  
  <hr>
  <h2>Liste des tâches</h2>
  <ul>
    <li v-for="task in tasks" :key="task">
      <input type="checkbox" name="">
      <span>{{ task }}</span>
    </li>
  </ul>
</template>


<script setup>
  import { ref } from 'vue'
  const name = ref('Luke')
  const taskNumber = ref(0)
  const taskName = ref('')
  const tasks = ref ([
    'first task',
    'second task'
  ])
  const addTask = () => {
    tasks.value.push(taskName.value)
    taskName.value = ''
  }
</script>


<style scss>

</style>
