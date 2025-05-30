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
        <div class="search-container">
            <input 
                type="text" 
                v-model="searchInput"
                placeholder="Search tasks..."
                class="search-input"
            >
        </div>
        <ul class="todo-list">
            <li v-for="(task, index) in filteredTasks" 
                :key="task.id"
                class="todo-item"
                :class="{'completed':task.completed}"
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
import { ref, computed, watch } from 'vue';

interface Task {
    id: number
    text: string;      
    completed: boolean; 
}

const tasks = ref<Task[]>([]) ;  // '' is the default value,  
              //  ^^^^^^  ^^
             //   |     |
            //    |     └── Initial value (empty array)
            //    └── Generic type parameter
const newTaskInput = ref<string> ('');
const searchInput = ref('');


const addTask = () => {
    if(newTaskInput.value.trim() !== '') {
        tasks.value.push({
            id: 1,
            text: newTaskInput.value,
            completed: false
        });
        console.log(tasks.value);
        
        newTaskInput.value = ''; //clear input after task is added
    }
}

const deleteTask = (id: number) => {
    tasks.value.splice(id, 1)
}


const filteredTasks = computed(() => {
    const searchTerm = searchInput.value.toLowerCase();
    return tasks.value.filter(task => 
        task.text.toLowerCase().includes(searchTerm)
    );
});

// watch(() => [searchTodoItem.value, tasks.value], () => {
//     const searchTerm = searchTodoItem.value.toLowerCase();
//     searchedTasks.value = tasks.value.filter(task => 
//         task.text.toLowerCase().includes(searchTerm)
//     );
// });

// When searchQuery is empty (''), this condition:
    // task.text.toLowerCase().includes('') will ALWAYS return true for every task ecause every string includes an empty string
      
    // Example:
    // "Buy milk".toLowerCase().includes('')  -> true
    // "Do homework".toLowerCase().includes('') -> true
    // "Any task".toLowerCase().includes('') -> true
    

/*
The filter() method creates a new array filled with elements that pass a test provided by a function.
The filter() method does not change the original array.

//Syntax
filter(callbackFn)
filter(callbackFn, thisArg)
The callback func, is to interate every element in the array. 
It should return a truthy value to keep the element in the resulting array, and a falsy value otherwise.
 The function is called with the following arguments: 
 - element: Current element being processed in the array
- index: current index being process in the array
- array: the array  filter() was called

*/


//enahance 
// Make filter for id, name, status

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

.search-container {
    margin-bottom: 1rem;
}

.search-input {
    width: 100%;
    padding: 0.8rem;
    border: 1px solid #e0e0e0;
    border-radius: 4px;
    font-size: 1rem;
    transition: border-color 0.2s;
}

.search-input:focus {
    outline: none;
    border-color: #4CAF50;
}
</style>