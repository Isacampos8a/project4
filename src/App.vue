<script setup>
import Header from './components/Header.vue';
import AddTask from './components/AddTask.vue';
import TaskList from './components/TaskList.vue';
import Clock from './components/Clock.vue';

import {ref, computed, onMounted, onUnmounted} from 'vue'

const tasks = ref([])

const handleTask = (taskData) => {
  tasks.value.push ({
    text: taskData.text,
    startTime: taskData.startTime,
    endTime: taskData.endTime
  })

  saveToLocalStorage()
}


const computeDuration = (startTime, endTime) => {
  const start = new Date(startTime)
  const end = new Date(endTime)

  const diffInMs = end - start

  const hours = Math.floor(diffInMs / (1000 * 60 * 60))
  const minutes = Math.floor((diffInMs % (1000 * 60 * 60)) / (1000*60))

  return `${hours} hours and ${minutes} minutes`
}

const formatTime = (date) => {
  const time = new Date(date)
  return time.toLocaleDateString([], {hour: '2-digit', minute: '2-digit'})
}



const taskWithDuration = computed(() => {
  return tasks.value.map(task => ({
    ...task,
    startTime: formatTime(task.startTime),
    endTime: formatTime(task.endTime),
    duration: computeDuration(task.startTime, task.endTime)
  }))
})

const handleDelete = (index) => {
  tasks.value.splice(index, 1);
  saveToLocalStorage()
}

const saveToLocalStorage = () => {
  localStorage.setItem('tasks', JSON.stringify(tasks.value))
}

onMounted(() => {
  const savedTasks = JSON.parse(localStorage.getItem('tasks'))

  if(savedTasks){
    tasks.value = savedTasks
  }
})



</script>

<template>
  <Header></Header>
  <Clock></Clock>
  <div class="container">
    <AddTask @taskSubmitted="handleTask" ></AddTask>
    <TaskList :tasks="taskWithDuration" @taskDeleted="handleDelete"></TaskList>

  </div>
  
</template>

