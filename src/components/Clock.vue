<script setup>
import {ref, onMounted, onUnmounted} from 'vue'

const currentTime = ref('')

const updateTime = () => {
    const now = new Date()
    currentTime.value = now.toLocaleTimeString([], {
        hour: '2-digit',
        minute: '2-digit'
    })
}

onMounted(() => {
    updateTime()
    const intervalID = setInterval(updateTime, 1000)

    onUnmounted(() => {
        clearInterval(intervalID)
    })
})


</script>

<template>
    <div class="clock">
        <h4>{{ currentTime }}</h4>

    </div>

</template>