<template>

<h1>{{ msg }}</h1>
<div class="wrapper">
    <h2> {{ title }}</h2>
    <h2>Number: {{ count }}</h2>
    <button @click="increment">Increment number by 1</button>
</div>

</template>

<script setup lang="ts">
import { onBeforeMount, onBeforeUnmount, onBeforeUpdate, onMounted, onUnmounted, onUpdated, ref, watch } from 'vue';

const msg = ref('Hello, Lifcyle Hooks!');
const title = ref('This is the title');
const count =  ref(1);

const increment = () => {
    count.value ++
}

console.log(`App component is setup`)

onBeforeMount (() => {
    console.log(`App component is before mount`)
})

//When element is already on DOM, it will 
onMounted (() => {
    console.log('This is on mounted');
    console.log(count.value);
})

//When DOM Tree changes, this one update first
onBeforeUpdate(() => {
    console.log('On Before Updated');
    console.log(count.value);
})


//Then this will call
onUpdated (() => {
    console.log('App is updated');
    console.log(count.value);
})

onBeforeUnmount(() => {
    console.log('Is before unMount');
})

onUnmounted(() =>{
    console.log('It on UnMounted');
})

watch(count, () => {
    console.log('This when count number changes!');
    
})

</script>

<style scoped>

h2 {
    color: white;
    font-weight: bold;
}
.wrapper {
    width: 100vw;
    height: 15vh;
    background-color: purple;
}

</style>