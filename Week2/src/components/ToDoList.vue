<template>
    <div class="todo-container">
        <form @submit.prevent="addTask" class="todo-form">
            <div class="input-group">
                <input 
                    type="text" 
                    id="newTask" 
                    v-model="newTaskInput"
                    placeholder="What needs to be done?"
                    class="todo-input"
                >
                <button type="submit" class="add-button">Add Task</button>
            </div>
        </form>
        <ul class="todo-list">
            <li v-for="(task, index) in tasks" 
                :key="index"
                class="todo-item"
                :class="task.completed ? 'completed' : ''"
            >
                <div class="todo-content">
                    <input 
                        type="checkbox" 
                        v-model="task.completed"
                        class="checkbox"
                    >
                    <span>{{ task.text }}</span>
                </div>
                <button @click="deleteTask(index)" class="delete-button">×</button>
            </li>
        </ul>
    </div>
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
        newTaskInput.value = ''; //clear input after task is added
    }
}

const deleteTask = (index: number) => {
    tasks.value.splice(index, 1)
}

</script>

<style scoped>
.todo-container {
    max-width: 600px;
    margin: 2rem auto;
    padding: 1rem;
    background: white;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.todo-form {
    margin-bottom: 2rem;
}

.input-group {
    display: flex;
    gap: 8px;
}

.todo-input {
    flex: 1;
    padding: 0.8rem;
    border: 1px solid #e0e0e0;
    border-radius: 4px;
    font-size: 1rem;
    transition: border-color 0.2s;
}

.todo-input:focus {
    outline: none;
    border-color: #4CAF50;
}

.add-button {
    padding: 0.8rem 1.5rem;
    background-color: #4CAF50;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.2s;
}

.add-button:hover {
    background-color: #45a049;
}

.todo-list {
    list-style: none;
    padding: 0;
    margin: 0;
}

.todo-item {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 1rem;
    margin-bottom: 0.5rem;
    background-color: #f8f9fa;
    border-radius: 4px;
    transition: all 0.2s;
}

.todo-item:hover {
    background-color: #f1f3f5;
}

.todo-content {
    display: flex;
    align-items: center;
    gap: 12px;
}

.checkbox {
    width: 18px;
    height: 18px;
    cursor: pointer;
}

.completed span {
    text-decoration: line-through;
    color: #868e96;
}

.delete-button {
    background: none;
    border: none;
    color: #ff6b6b;
    font-size: 1.2rem;
    cursor: pointer;
    padding: 0.2rem 0.5rem;
    border-radius: 4px;
    transition: background-color 0.2s;
}

.delete-button:hover {
    background-color: #ffe3e3;
}
</style>