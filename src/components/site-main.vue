<script setup>
import { ref, onMounted, onBeforeUnmount, watchEffect } from 'vue';
import { getapi } from '../middleware/getapi.js';

const getbio = ref(null);
const showDownArrow = ref(true);

watchEffect(async () => {
  console.log('Fetching data...');
  try {
    const data = await getapi('getbio');
    console.log('Data fetched:', data);
    getbio.value = data;
  } catch (error) {
    console.error('Error fetching data:', error);
  }
});

const handleScroll = () => {
  showDownArrow.value = window.pageYOffset === 0;
};

onMounted(() => {
  window.addEventListener('scroll', handleScroll);
});

onBeforeUnmount(() => {
  window.removeEventListener('scroll', handleScroll);
});
</script>

<template>
  <div id="root">
    <div id="background" class="background">
      <div class="background-image"></div>
    </div>
    <div class="banner">
      <div class="avatar">
        <img src="@/assets/logo.png" alt="avatar" />
      </div>
      <div class="title">
        <div class="name">
          <img src="@/assets/cwtc.svg" />
        </div>
        <div class="bio">{{ getbio }}</div>
      </div>
    </div>
    <div class="down-arrow" v-show="showDownArrow">
      <div class="down-arrow-inner">
        <svg stroke="currentColor" fill="currentColor" stroke-width="0" viewBox="0 0 512 512" height="1em" width="1em"
          xmlns="http://www.w3.org/2000/svg">
          <path fill="none" stroke-linecap="round" stroke-linejoin="round" stroke-width="48" d="M112 184l144 144 144-144">
          </path>
        </svg>
      </div>
    </div>
  </div>
</template>

<style scoped>
.down-arrow-inner {
  animation: arrow-bounce 2s infinite;
}

@keyframes arrow-bounce {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-20px);
  }
}
</style>