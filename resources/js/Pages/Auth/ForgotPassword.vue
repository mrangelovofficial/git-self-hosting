<script setup>
import FrontLayout from '@/Layouts/FrontLayout.vue';
import InputError from '@/Components/InputError.vue';
import AuthButton from '@/Components/Auth/AuthButton.vue';
import TextInput from '@/Components/Auth/TextInput.vue';
import { Head, Link, useForm } from '@inertiajs/inertia-vue3';

defineProps({
    status: String,
});

const form = useForm({
    email: '',
});

const submit = () => {
    form.post(route('password.email'));
};
</script>

<template>
    <FrontLayout>
        <Head title="Forgot Password" />

        <h2 class="font-bold pt-10 text-4xl">Forgot password?</h2>
        <p class="text-gray-500 text-md mt-1 mb-6">No worries. We'll send you reset instructions.</p>

        <div v-if="status" class="mb-4 font-medium text-sm text-green-600">
            {{ status }}
        </div>

        <form @submit.prevent="submit">
            <div>
                <TextInput id="email" type="email" class="mt-1 block w-full" placeholder="Email" v-model="form.email" required autofocus autocomplete="username" />
                <InputError class="mt-2" :message="form.errors.email" />
            </div>

            <div class="flex items-center justify-end mt-4">
                <AuthButton :class="{ 'opacity-25': form.processing }" :disabled="form.processing">
                    Send Reset Instructions 
                </AuthButton>
            </div>
            <Link :href="route('login')" class="flex text-gray-500 justify-center mt-6 gap-x-2">
                <span> ← </span>
                <span>Back to log in</span>
            </Link>
            
        </form>
    </FrontLayout>
</template>
