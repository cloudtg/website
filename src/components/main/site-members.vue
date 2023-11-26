<script setup>
import { ref, watchEffect } from 'vue';
import { getapi } from '@/middleware/getapi.js';
import ContactInfo from '@/lib/ContactInfo.vue';

const membersData = ref(null);

watchEffect(async () => {
    console.log('Fetching data...');
    try {
        const data = await getapi('getmembers');
        membersData.value = data.data;
    } catch (error) {
        console.error('Error fetching data:', error);
    }
});
</script>

<template>
    <main class="members-card">
        <section class="py-16">
            <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
                <h2 class="text-3xl font-extrabold text-gray-900 mb-6">Members</h2>
                <div class="grid grid-cols-3 gap-6">
                    <div v-for="member in membersData" :key="member.id"
                        class="overflow-hidden shadow rounded-lg bg-white bg-opacity-20 backdrop-blur flex flex-col items-center p-4">
                        <img :src="member.image" :alt="`Profile of ${member.name}`"
                            class="w-16 h-16 object-cover rounded-full mb-4" />
                        <div class="text-center">
                            <h3 class="text-xl font-semibold">{{ member.name }}</h3>
                            <p class="mt-2 text-sm text-white">{{ member.description }}</p>
                        </div>
                        <contact-info :contacts="member.contact"></contact-info>
                    </div>
                </div>
            </div>
        </section>
    </main>
</template>
