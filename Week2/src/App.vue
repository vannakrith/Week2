<template>
  <header>
  </header>
  <main>
    <div class="wrapper">
      <!-- <VIf/> -->
       <ToDoList/>
      <!-- <UnderstandArrayGenericSyntax/> -->
      <!-- <ComputedProperty/> -->
       <!-- <LifeCyleHook/> -->
    </div>

  </main>
</template>

<script setup>
  import VIf from './components/TemplateSyntaxBasic.vue';
  import ToDoList from './components/ToDoList.vue'
  import UnderstandArrayGenericSyntax from './components/UnderstandArrayGenericSyntax.vue'
  import ComputedProperty from './components/ComputedProperty.vue'
  import LifeCyleHook from './components/LifeCycleHook.vue'
import { onMounted } from 'vue';


</script>

<style scoped>


</style>
