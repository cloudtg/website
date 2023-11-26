<script setup>
defineProps(['provider']);

import { ref } from 'vue';
const year = ref(String(new Date().getFullYear()));
</script>

<template>
  <main id="footer">
    <footer class="site-footer text-gray-300 py-6">
      <div class="container mx-auto px-4 flex justify-between items-center">
        <div>
          <p class="mt-2 text-sm">© {{ year }} 云游科社</p>
          <p class="mt-2 text-sm">Page made by TiaNXianG(iykrzu)</p>
        </div>
        <div>
          <p class="mt-2 text-sm">本期主题照片由 {{ provider }} 提供</p>
        </div>
      </div>
    </footer>
  </main>
</template>
