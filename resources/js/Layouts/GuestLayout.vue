<script setup>
import ApplicationLogo from '@/Components/ApplicationLogo.vue';
import { Link } from '@inertiajs/vue3';
</script>

<template>
    <div class="overflow-auto w-screen h-screen bg-gray-100 p-4 flex justify-center items-center">
        <slot />
    </div>
</template>