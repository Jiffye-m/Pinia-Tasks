<template>
    <div class="task">
    <h3>{{ task.title }}</h3>

    <div class="icons">
        <i class="material-icons" @click="taskStore.deleteTask(task.id)">delete</i>
        <i :class="{active: task.isFav}"  class="material-icons" @click="taskStore.toggleFav(task.id)">favorite</i>
    </div>

    </div>
</template>

<script setup>
import {ref, defineProps} from 'vue'
import { useTaskStore } from '../stores/TaskStore';

const props = defineProps(['task'])

const taskStore = useTaskStore()

</script>

<style scoped>

</style>