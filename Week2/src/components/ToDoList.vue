<template>
    <div class="wrapper">
        <form @submit.prevent="addTask">
            <label for="newTask">Add new Task</label>
            <input type="text" id="newTask" v-model="newTaskInput">
            <button type="submit">Add Task</button>
        </form>
    </div>
    <ul>
        <li v-for="(task, index) in tasks" :key="index">
            <input type="checkbox" v-model="task.completed">
            <span :class="{ completed: task.completed }">{{ task.text }}</span>
            <span :class="task.completed ? 'complete' : ''">{{ task.text }}</span>
            <button @click="deleteTask(index)">x</button>
        </li>
    </ul>
</template>

<script setup lang="ts">
import { ref } from 'vue';

interface Task {
    text: string;      
    completed: boolean; 
}

const tasks = ref<Task[]>([]) ;  // '' is the default value, 
              //  ^^^^^^  ^^
             //   |     |
            //    |     └── Initial value (empty array)
            //    └── Generic type parameter
const newTaskInput = ref<string> ('');

const addTask = () => {
    if(newTaskInput.value.trim() !== '') {
        tasks.value.push({
            text: newTaskInput.value,
            completed: false
        });
        newTaskInput.value = ''; //clear input after task added
    }
}

const deleteTask = (index: number) => {
    tasks.value.splice(index, 1)
}

</script>

<style scoped>

.complete {
    text-decoration: line-through;
}

</style>