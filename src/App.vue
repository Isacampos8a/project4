<script setup>
import Header from './components/Header.vue';
import AddTask from './components/AddTask.vue';
import TaskList from './components/TaskList.vue';

import {ref, computed} from 'vue'

const tasks = ref([])

const handleTask = (taskData) => {
  tasks.value.push ({
    text: taskData.text,
    startTime: taskData.startTime,
    endTime: taskData.endTime
  })
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
  return time.toLocaleTimeString([], {hour: '2-digit', minute: '2-digit'})
}



const taskWithDuration = computed(() => {
  return tasks.value.map(task => ({
    ...task,
    startTime: formatTime(task.startTime),
    endTime: formatTime(task.endTime),
    duration: computeDuration(task.startTime, task.endTime)
  }))
})


</script>

<template>
  <Header></Header>


  <div class="container">
    <AddTask @taskSubmitted="handleTask" ></AddTask>
    <TaskList :tasks="taskWithDuration"></TaskList>
  </div>
  
</template>

