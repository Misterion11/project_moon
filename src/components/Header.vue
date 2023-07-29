<template>
  <header class="bg-purple-900 p-4 flex items-center">
    <img src="/src/assets/butterfly.png" class="w-16" alt="">
    <h1 class="text-4xl text-white font-bold ml-4 w-full flex justify-center pr-20">{{ title }}</h1>
  </header>
</template>



<script setup lang="ts">
import { ref } from 'vue';

const title = ref('Yorunochō');
</script>
