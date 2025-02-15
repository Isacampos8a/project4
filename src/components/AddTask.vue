<script setup>
    import {ref, defineEmits} from 'vue'

    const text = ref ('')
    const startTime = ref ('')
    const endTime = ref ('')


    const emit = defineEmits([
        'taskSubmitted'
    ])

    const onSubmit = () => {
        const taskData = {
            text: text.value,
            startTime: new Date(startTime.value),
            endTime: new Date(endTime.value),
        }

        emit('taskSubmitted', taskData)
        

        text.value = ''
        startTime.value = ''
        endTime.value = ''
    }

</script>

<template>
    <h3>Add New Task</h3>
    <form id="form" @submit.prevent="onSubmit">
        <div class="form-control">
            <label for="task-name">Task Name</label>
            <input type="text" id="text" v-model="text" placeholder="Enter Task...">
        </div>
        <div class="form-control">
            <label for="start-time">Start Time</label>
            <input type="datetime-local" id="start-time" v-model="startTime" placeholder="Enter Start Time...">
        </div>
        <div class="form-control">
            <label for="end-time">End Time</label>
            <input type="datetime-local" id="end-time" v-model="endTime" placeholder="Enter End Time...">
        </div>
        <button class="btn">Add Task</button>
    
    
    
    </form>
</template>