<script setup>
import { onMounted, ref } from 'vue';

defineProps(['modelValue']);

defineEmits(['update:modelValue']);

const input = ref(null);

onMounted(() => {
    if (input.value.hasAttribute('autofocus')) {
        input.value.focus();
    }
});
</script>

<template>
    <input class="border-gray-400 border-t-0 border-x-0 border-b focus:outline-0 focus:ring-0 focus:border-yellow-500" :value="modelValue" @input="$emit('update:modelValue', $event.target.value)" ref="input">
</template>
