<template>

<div>
    <p>This is username: {{ fullName }}</p>
</div>

<div class="form">
    <form >
        <label for="username">Username</label>
        <input type="text" v-model="username">
        <label for="password">Password</label>
        <input type="text" v-model="password">
        <button :disabled="!validationForm">Submit</button>
    </form>
</div>

<div class="filter-list">
    <br>
    <h2>2. This is to show filter using Computed Property</h2>
    <input type="text" name="input" id="input" v-model="searchQuery" placeholder="Search...">
    <ul>
        <li v-for="(product, index) in filterProducts" :key="index">
            {{ product.name }}
        </li>
    </ul>
</div>

</template>

<script setup lang="ts">
import { computed, ref } from 'vue';

//enable/ disable submit button based on 
/* 
What is computed property?
it is like a smart variable, automatically updates when the things it depends on change
- It's derived from other data
- It's reactive, updae only when needed
- It's like formula that update itself when sth change

*/

const firstName = ref('Vannak');
const lastName = ref('Rith');

const fullName = computed (() => {
    return `${firstName.value} ${lastName.value}`
})

//More example
// 1. Use with enable/disable submit button depends on form validation

const password = ref('');
const username = ref('');
const validationForm = computed(() => {
  return  username.value.trim() !== '' && password.value.length >= 6;
})

//2. Use with filter a list

interface IProductList {
    id: number,
    name: string
}

const searchQuery = ref('');
const productList = ref<IProductList[]>([
    {id: 1, name: 'iPhone'},
    {id: 2, name: 'Samsung'},
    {id: 3, name: 'Oppo'},
]);

const filterProducts = computed (() => {
    return productList.value.filter(p => 
        p.name.toLowerCase().includes(searchQuery.value.toLowerCase())
    );
});


</script>

<style scoped>
.form {
    display: flex;
    flex-direction: column;
}

</style>