<script setup>
defineProps({
    type: {
        type: String,
        default: 'submit',
    },
});
</script>

<template>
    <button :type="type" class="block w-full py-3 bg-yellow-500 border border-transparent rounded-lg text-sm font-semibold text-white tracking-widest hover:bg-yellow-700 active:bg-yellow-900 focus:outline-none active:border-yellow-900 focus:shadow-outline-gray transition ease-in-out duration-150">
        <slot />
    </button>
</template>
