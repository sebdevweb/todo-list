<template>
  <form action="" @submit.prevent="addToDo">
    <fieldset role="group">
      <input 
      v-model="newTodo"
        type="text"
        placeholder="Tâche à effectuer"
      >
      <button :disabled="newTodo.length == 0">Ajouter</button>
    </fieldset>
  </form>
  <div v-if="todos.length == 0">Vous n'avez pas de tâches à faire :(</div>
  <div v-else>
    <ul>
      <li 
        v-for="todo in sortedTodos"
        :key="todo.date"
        :class="{completed: todo.completed}"
      >
      <label>
        <input 
          type="checkbox" 
          name="" 
          id=""
          v-model="todo.completed"
        >
        {{ todo.title }}
      </label>
      </li>
    </ul>
    <label>
      <input 
        type="checkbox" 
        name="" 
        id=""
        v-model="hideCompleted"
      >
      Masquer les tâches complétées.
    </label>
    <p v-if="remainigTodos > 0">
      {{ remainigTodos }} tâche{{ remainigTodos > 1 ? 's' : '' }} restante{{ remainigTodos > 1 ? 's' : '' }}.
    </p>
  </div>
</template>


<script setup>
  import { ref, computed } from 'vue'

  const todos = ref([{
    title: 'Tâche de test',
    completed: true,
    date: 1
  }, {
    title: 'Tâche à faire',
    completed: false,
    date: 2
  }])
  const newTodo = ref('')
  const hideCompleted = ref(false)

  const addToDo = () => {
    //console.log('test');
    todos.value.push({
      title: newTodo.value,
      completed: false,
      date: Date.now()
    })
    newTodo.value = ''
  }

  const sortedTodos = computed(() => {
    console.log('test')
    const sortedTodos =  todos.value.toSorted((a, b) => a.completed > b.completed ? 1 : -1)
    if (hideCompleted.value == true) {
      return sortedTodos.filter(t => t.completed == false)
    }
    return sortedTodos
  })

  const remainigTodos = computed(() => {
    return todos.value.filter(t => t.completed == false).length
  })
</script>


<style>
  .completed {
    opacity: .5;
    text-decoration: line-through;
  }
</style>