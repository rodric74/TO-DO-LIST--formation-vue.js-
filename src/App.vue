<template>
   <Layout>
      <template #header>
        <h1>TO-DO LIST</h1>
      </template>
      <template #aside>
        SideBar
      </template>
      <template #main>
        Main</template>
      <template #footer>
        Footer</template>
   </Layout>



  <p v-if="tasks.length === 0">Il n'y a pas de tache à effectuer</p>
  <form action="" @submit.prevent="addTask">
    <input type="text" v-model="newTask" placeholder="ajouter un truc à faire">
    <button :disabled="newTask.length === 0">Azy ajoute</button>
    </form>
    <ul>
      <li v-for="task in sortTasks" 
          :key="task.id" 
          :class="{done: task.isDone}">
          <Checkbox :label="task.title" v-model="task.isDone" />
      </li>
    </ul>
 
  <div>
    <label for="">
    <input type="checkbox" v-model="hideDone">
    Cacher les taches faites
    </label>
    <p>{{ remainingTasks }} tâche {{ remainingTasks > 1 ? 's' : '' }} à faire</p>
    <Checkbox label="Bonjour"/>
  </div>
</template>

<script setup>
import { computed,ref } from 'vue'
import Checkbox from './Checkbox.vue'
import Button from './Button.vue'
import Layout from './Layout.vue'

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

}

const sortTasks = computed(
  () => {
    console.log('Demo')
  const sortedTasks = tasks.value.toSorted((a, b) => a.isDone > b.isDone ? 1 : -1)
  if (hideDone.value === true) {
    return sortedTasks.filter(t => t.isDone === false)
  }
  return sortedTasks
}
)
// console.log(sortTasks.value)

const remainingTasks = computed(() => {
  return tasks.value.filter(t => !t.isDone).length
})
</script>

<style>
.done{
  text-decoration: line-through;
  color: blue;
}
</style>