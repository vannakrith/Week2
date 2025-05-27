<template>
<div>
  <h3>Generic Array Syntax Examples</h3>
  <pre>Check console for examples</pre>
</div>
</template>

<script setup lang="ts">
import { ref } from 'vue';

// Syntax Pattern 1: Using Array<Type>
const numbers1: Array<number> = [1, 2, 3];
const numsdfdf : Array<number> = [];
const number133 : Array<number> = [1,2,3,4,4,4,4,];
  
  const numer1: Array<number> = [1, 3,3,4];
    const num2 : number[] = [1,2];
    // Syntax Pattern 2: Using Type[]
    const numbers2: number[] = [1, 2, 3];
    
    const number223 : number[] = [];
    const numsfdsf : number[] = [];


// Syntax Pattern 3: Generic array with interface
interface Person {
  name: string;
  age: number;
}
const people: Person[] = [
  { name: "John", age: 30 }
];

//using Array<Type> 
const peopl1 : Array<Person> = [
  {name: 'Vannak', age: 22}
]


// Syntax Pattern 4: Reactive generic array in Vue
const reactiveArray = ref<string[]>([]);

const reactiveArray1 = ref<number[]>([1])
const reactiveArrayString = ref<string[]> ([]);

// Log examples
console.log({ numbers1, numbers2, people, reactiveArray, peopl1, numsfdsf });
</script>

<style>

</style>