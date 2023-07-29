<script setup
  lang="ts">
  import {
    ref,
    onMounted,
    onBeforeUnmount,
    watch
  } from 'vue';
  const {
    label,
    options
  } = defineProps < {
    label: string;
    options: string[];
  } > ();
  const isMobile = ref(false);
  const showList = ref(false);

  function checkIsMobile() {
    isMobile.value = window.innerWidth <= 768;
  }
  onMounted(() => {
    checkIsMobile();
    window.addEventListener('resize', checkIsMobile);
  });
  onBeforeUnmount(() => {
    window.removeEventListener('resize', checkIsMobile);
  });
  watch(isMobile, () => {});

  function toggleList() {
    showList.value = !showList.value;
  }

  const getAudioPath = (option: string) => {
    if(option === 'Le papillon et la lune')
      return 'https://www.dropbox.com/s/xgd38bjl5w1l8pd/Le_papillon_et_la_lune.mp3' + '?raw=1'
  };

</script>

<template>
  <div class="my-4">
    <button class="mb-2" @click="toggleList"
      :class="[
        'py-4 px-8 rounded-md text-lg font-medium',
        isMobile ? 'w-full' : 'w-80',
        'bg-purple-700 text-white hover:opacity-75 cursor-pointer',
        isMobile ? 'text-xl' : 'w-80 h-40 text-3xl'
      ]">
      {{ label }}
    </button>
    <div>
      <ul v-if="showList"
      class="text-white mt-0">
      <li class="text-center mb-4" v-for="option in options"
        :key="option">
        <span class="text-xl">{{ option }}</span>
        <div class="flex justify-center md:justify-start">
          <audio :key="option" class="w-80 md:w-80 p-2 bg-gray-300 rounded" controls :src="getAudioPath(option)"></audio>
        </div>
      </li>
    </ul>
    </div>
  </div>
</template>
