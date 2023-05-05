<template>
  <main>

<!-- Heading -->

<header>
  <img src="./assets/pinia-logo.svg" alt="pinia-logo">
  <h1>Pinia Tasks</h1>
</header>


<!-- Add Task Form -->
<div class="new-task-form">
<TaskForm />
</div>

<!-- Filter -->

<nav class="filter">
  <button @click="filter = 'all'">All Tasks</button>
  <button @click="filter = 'favs'">Fav Tasks</button>
</nav>


<!-- Loading -->

<div v-if="loading" class="loading">
  Loading Tasks........
</div>

<!--  task lists  -->

<div class="task-list" v-if="filter === 'all'" >
  <p>You have {{ totalCount }}</p>
  <div v-for="task in tasks" :key="task.id">
      <TaskDetails :task="task"/>
  </div>
</div>

<div class="task-list" v-if="filter === 'favs'" >
  <p>You have {{ favCount }}</p>
  <div v-for="task in favs" :key="task.id">
      <TaskDetails :task="task"/>
  </div>
</div>


<!-- reset button -->
<div class="filter">
<button @click="taskStore.$reset">RESET</button>
</div>


  </main>
</template>

<script setup>
import { storeToRefs } from 'pinia'
import { ref } from 'vue'
import TaskDetails from './components/TaskDetails.vue'
import TaskForm from './components/TaskForm.vue'
import  { useTaskStore }  from './stores/TaskStore'

const taskStore = useTaskStore()

// converting getters to refs
const { tasks, loading, favs, totalCount, favCount } = storeToRefs(taskStore)

// fetch tasks
taskStore.getTasks()


const filter = ref('all')


</script>

<style scoped>


</style>
