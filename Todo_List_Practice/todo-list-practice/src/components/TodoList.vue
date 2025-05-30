<template>

<div class="container">
   <form @submit.prevent="addToDoList">
        <input v-model="todoInput" type="text" placeholder="Add to do...">
        <button>Add to do</button>
    </form>
    <div class="search-items">
     <input v-model="searchTodoInput" type="text" placeholder="Search item...." >
    </div>
   <div class="to-do-items">
        <ul v-for="task in searchTodo" 
            :key="task.id">
            <li>
                <input type="checkbox" v-model="task.isComplete">
                <span :class="{'completed' : task.isComplete}">{{ task.name }}</span>
                <button @click="removeTodo(task.id)">x</button>
            </li>

        </ul>
   </div>
</div>

</template>

<script setup lang="ts">
import { computed } from '@vue/reactivity';
import { ref, watch } from 'vue';

interface ITodo {
    id: number,
    name: string,
    isComplete: boolean
}

const todoInput = ref<string>('');
const tasks = ref<ITodo[]>([]);
const searchTodoInput = ref<string>('');

let nextId = 1;
const addToDoList = () => {
    const newTask = {
        id: nextId++,
        name: todoInput.value,
        isComplete: false
    };
    tasks.value.push(newTask)
    todoInput.value = ''; 
    console.log('task added:', tasks.value);
    
}

const removeTodo = (taskId: number) => {
    tasks.value = tasks.value.filter(task => task.id !== taskId)
}

const searchTodo = computed (() => {
    const searchCondition = searchTodoInput.value.toLowerCase();
    return tasks.value.filter( task => 
        task.name.includes(searchCondition)
    )
})

</script>

<style scoped>

.completed {
    text-decoration: line-through;
}

</style>