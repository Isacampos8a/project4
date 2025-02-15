<script setup>
    import {defineProps} from 'vue'

    defineProps({
        tasks: {
            type: Array,
            required: true,
        }
    })


</script>

<template>
    <h3>Task List</h3>
    <ul id="list" class="list">
        <li v-for="(task, index) in tasks" :key="index">
            Task: {{ task.text }}<br />
            Start Time: {{  task.startTime }}<br />
            End Time: {{ task.endTime }}<br />
            Time Duration: {{ task.duration }}
        </li>
    </ul>


</template>