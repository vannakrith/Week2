<template>
    <div class="container">
        <div class="form">
            <form @submit.prevent="addTodo">
                <input v-model="addTodoInput" type="text" placeholder="Add todo....">
                <button>Add Todo</button>
            </form>
        </div>
        <div class="todo-display">
            <ul v-for="task in taskArr" :key="task.id">
                <li>
                    <input v-model="task.isComplete" type="checkbox">
                    <span :class = "{completed: task.isComplete}">{{ task.text }}</span>
                    <button @click="removedTodoList(task.id)">x</button>
                </li>
            </ul>
            <div v-if="taskArr.length === 0">No task</div>
        </div>
    </div>
</template>

<script setup lang="ts">
import { ref } from 'vue';
const addTodoInput = ref<string>('');
interface ITodo {
    id: number,
    text: string,
    isComplete: boolean
}
const taskArr = ref <ITodo[]>([]); 

let nextTodoId = 1;
const addTodo = () => {
        taskArr.value.push( {
        id: nextTodoId++,
        text: addTodoInput.value,
        isComplete: false
    })
    addTodoInput.value = '';
    console.log('task when add: ', taskArr.value);
}

const removedTodoList = (taskId: number) => {
    taskArr.value = taskArr.value.filter (task => 
        task.id !== taskId
    )
}

</script>

<style scoped>

.completed {
    text-decoration: line-through;
}

</style>