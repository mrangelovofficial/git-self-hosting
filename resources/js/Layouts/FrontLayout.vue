<script setup>
import ApplicationLogo from '@/Components/ApplicationLogo.vue';
import { Link } from '@inertiajs/inertia-vue3';
</script>

<template>
    <div class="flex w-full h-screen">
        <div class="w-full lg:w-5/12 py-6 px-14">
            <Link href="/">
                <ApplicationLogo class="h-8 mb-20 fill-current text-gray-900" />
            </Link>
            <div class="md:w-9/12 max-w-md mx-auto">
                <slot />
            </div>
        </div>
        
        <div
        class="w-7/12 hidden lg:flex items-center rounded-l-3xl bg-cover bg-center bg-no-repeat"
        style="background-image: url('/assets/images/auth-bg.jpg')">
        </div>

    </div>
</template>
