<script setup>
defineProps({
    type: {
        type: String,
        default: 'submit',
    },
});
</script>

<template>
    <button
        :type="type"
        class="bg-blue-800 p-1 rounded text-white"
    >
        <slot />
    </button>
</template>