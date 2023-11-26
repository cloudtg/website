<script setup>
defineProps({
    contacts: {
        type: Object,
        required: true
    }
});
</script>

<template>
    <div class="contact-info">
        <template v-for="(value, key) in contacts" :key="key">
            <p class="inline-block text-white">
                <span v-if="key === 'website'">
                    <a :href="value" class="ri-global-line ri-2x text-white"></a>
                </span>
                <span v-else-if="key === 'twitter'">
                    <a :href="value" class="ri-twitter-line ri-2x text-white"></a>
                </span>
                <span v-else-if="key === 'email'">
                    <a :href="`mailto:${value}`" class="ri-mail-line ri-2x text-white"></a>
                </span>
                <span v-else-if="key === 'github'">
                    <a :href="value" class="ri-github-line ri-2x text-white"></a>
                </span>
                <span v-else-if="key === 'telegram'">
                    <a :href="value" class="ri-telegram-line ri-2x text-white"></a>
                </span>
                <span v-else-if="key === 'line'">
                    <a :href="value" class="ri-line-line ri-2x text-white"></a>
                </span>
            </p>
        </template>
    </div>
</template>
