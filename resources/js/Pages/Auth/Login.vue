<script setup>
import Checkbox from '@/Components/Checkbox.vue';
import GuestLayout from '@/Layouts/GuestLayout.vue';
import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import AuthButton from '@/Components/Auth/AuthButton.vue';
import TextInput from '@/Components/Auth/TextInput.vue';
import FacebookButton from '@/Components/Auth/FacebookButton.vue';
import { Head, Link, useForm } from '@inertiajs/inertia-vue3';

defineProps({
    canResetPassword: Boolean,
    status: String,
});

const form = useForm({
    email: '',
    password: '',
    remember: false
});

const submit = () => {
    form.post(route('login'), {
        onFinish: () => form.reset('password'),
    });
};
</script>

<template>
    <GuestLayout>
        <Head title="Log in" />
        <h2 class="font-bold text-4xl">Welcome back,</h2>
        <p class="text-gray-500 text-md mt-1 mb-6">Continue with Facebook or enter your details.</p>
        
        <FacebookButton />

        <div class="flex items-center gap-x-5 my-5">
            <div class="w-full h-1 border-gray-200 border-b"></div>
            <div class="text-gray-600 text-xs">OR</div>
            <div class="w-full h-1 border-gray-200 border-b"></div>
        </div>

        <div v-if="status" class="mb-4 font-medium text-sm text-green-600">
            {{ status }}
        </div>

        <form @submit.prevent="submit">
            <div>
                <TextInput id="email" type="email" placeholder="Email" class="mt-1 block w-full" v-model="form.email" required autofocus autocomplete="username" />
                <InputError class="mt-2" :message="form.errors.email" />
            </div>

            <div class="mt-4">
                <TextInput id="password" type="password" placeholder="Password" class="mt-1 block w-full" v-model="form.password" required autocomplete="current-password" />
                <InputError class="mt-2" :message="form.errors.password" />
            </div>

            <div class="flex flex-col-reverse gap-y-4 sm:gap-y-0 sm:flex-row sm:justify-between mt-5">
                <label class="flex items-center">
                    <Checkbox name="remember" v-model:checked="form.remember" />
                    <span class="ml-2 text-sm text-gray-700 font-medium tracking-wide">Remember for 30 days</span>
                </label>

                <Link v-if="canResetPassword" :href="route('password.request')" class="underline text-sm text-gray-900 font-medium">
                    Forgot password?
                </Link>
            </div>

            <div class="block mt-8">
                

                <AuthButton :class="{ 'opacity-25': form.processing }" :disabled="form.processing">
                    Log In
                </AuthButton>
            </div>
        </form>
    </GuestLayout>
</template>
