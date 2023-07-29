<script setup
  lang="ts">
  import Header from './components/Header.vue';
  import Button from './components/Button.vue';
  import {
    ref,
    onMounted
  } from 'vue';
  const headerHeight = ref(0);
  const isMobile = ref(false);
  onMounted(() => {
    const headerElement = document.querySelector('header');
    if (headerElement) {
      headerHeight.value = headerElement.clientHeight;
    }
    const handleResize = () => {
      isMobile.value = window.innerWidth < 768;
    };
    window.addEventListener('resize', handleResize);
    handleResize();
  });
</script>

<template>
  <div class="flex flex-col h-screen">
    <Header :class="{'mb-8': isMobile, 'mb-16': !isMobile}"></Header>
    <div :class="{'flex-grow flex justify-evenly': !isMobile, 'flex flex-col flex-grow': isMobile}">
      <Button label="Raconte moi une histoire !"
        :options="['Le papillon et la lune', 'Histoire 2', 'Histoire 3']" />
      <Button label="Ôte-moi d'un doute"
        :options="['Option 1', 'Option 2', 'Option 3']" />
      <Button label="Que faire quand..."
        :options="['Option 1', 'Option 2', 'Option 3']" />
    </div>
  </div>
</template>
