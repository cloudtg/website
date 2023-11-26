<script setup>
import { ref, watchEffect } from 'vue';
import { getapi } from '@/middleware/getapi.js';
import SiteMain from './components/main/site-main.vue';
import SiteMembers from './components/main/site-members.vue';
import SiteFooter from './components/main/site-footer.vue';

// Define bg_provider outside of watchEffect
const bg_provider = ref(null);

watchEffect(async () => {
  console.log('Fetching data...');
  try {
    const img_data = await getapi('getimg');
    console.log('Data fetched:', img_data);
    document.documentElement.style.setProperty('--bg_img', `url(${img_data.image})`);
    bg_provider.value = img_data.provider;
  } catch (error) {
    console.error('Error fetching data:', error);
  }
});
</script>

<template>
  <!-- 标题界面 -->
  <SiteMain />
  <!-- 成员界面 -->
  <SiteMembers />
  <!-- 页脚 -->
  <SiteFooter :provider="bg_provider" />
</template>
