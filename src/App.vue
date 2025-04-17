<template>
  <div>
  <p v-if="tasks.length === 0">Il n'y a pas de tache à effectuer</p>
  <form action="" @submit.prevent="addTask">
    <input type="text" v-model="newTask" placeholder="ajouter un truc à faire">
    <button :disabled="newTask.length === 0">Azy ajoute</button>
    </form>
    <ul>
      <li v-for="task in sortTasks()" :key="task.id" :class="{done: task.isDone}">
        <span>{{ task.title }}</span>
        <input type="checkbox" v-model="task.isDone" @change="sortTasks()">
      </li>
    </ul>
  </div>
  <div>
    <label for="">
    <input type="checkbox" v-model="hideDone">
    Cacher les taches faites
    </label>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const newTask = ref('')
const tasks = ref([])
const hideDone = ref(false)

const addTask = () => {
  if (newTask.value.trim() === '') return
  const task = { 
    id: Date.now(), 
    title: newTask.value, 
    isDone: false 
  }
  tasks.value.push(task)
  newTask.value = ''
  sortTasks()
}

const sortTasks = () => {
  const sortedTasks = tasks.value.toSorted ((a, b) => a.isDone > b.isDone ? 1 : -1)
  if (hideDone.value === true) {
    return sortedTasks.filter(t => t.isDone === false)
  }
  return sortedTasks
}
  

</script>

<style>
.done{
  text-decoration: line-through;
  color: blue;
}
</style>