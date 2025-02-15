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

const taskWithDuration = computed(() => {
  return tasks.value.map(task => ({
    ...task,
    duration: computeDuration(task.startTime, task.endTime)

  }))
})

const computeDuration = (startTime, endTime) => {
  const start = new Date(startTime)
  const end = new Date(endTime)

  const diffInMs = end - start

  const hours = Math.floor(diffInMs / (1000 * 60 * 60))
  const minutes = Math.floor((diffInMs % (1000 * 60 * 60)) / (1000*60))

  return `${hours} hours and ${minutes} minutes`
}


</script>

<template>
<Header></Header>
<AddTask @taskSubmitted="handleTask" ></AddTask>
<TaskList :tasks="taskWithDuration"></TaskList>

</template>

