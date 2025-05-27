<template>
    <div v-if="status === 'active'">Hi, User {{ name }} is active</div>
    <div v-else-if="status === 'inactive'">User {{ name }} is inactive</div>
    <div v-else>User {{ name }} is pending</div>
    <div v-for="task in tasks" :key="id">{{ task.name }}</div>
    <h2>Atribute binding: </h2>
    <!-- <a v-bind:href="links">Click here</a> -->
    <a :href="links">Click here, short bind:</a>
    <br/>
    <button @click="toggleStatus">Toggle status</button>
</template>

<script setup>
import { ref } from 'vue';


const name = 'Vannak';
const status = ref('active');

const tasks = [
    {id: 1, name: 'task1'},
    {id: 2, name: 'task2'},
    {id: 3, name: 'task3'},
];

const links = 'https://www.google.com/';

const toggleStatus = () => {
    if(status.value === 'active') {
        status.value = 'inactive'
    }
    else {
        status.value = 'active';
    }
}

</script>

<style>

</style>