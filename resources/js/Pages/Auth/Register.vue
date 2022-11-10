<script setup>
import FrontLayout from '@/Layouts/FrontLayout.vue';
import InputError from '@/Components/InputError.vue';
import AuthButton from '@/Components/Auth/AuthButton.vue';
import TextInput from '@/Components/Auth/TextInput.vue';
import { Head, Link, useForm } from '@inertiajs/inertia-vue3';

const form = useForm({
    name: '',
    email: '',
    password: '',
    password_confirmation: '',
    terms: false,
});

const submit = () => {
    form.post(route('register'), {
        onFinish: () => form.reset('password', 'password_confirmation'),
    });
};
</script>

<template>
    <FrontLayout>
        <Head title="Register" />
        <h2 class="font-bold text-4xl">Create your account</h2>
        <p class="text-gray-500 text-md mt-1 mb-6">Already have an account?
            <Link :href="route('login')" class="underline text-sm text-yellow-600">
                Log in
            </Link>
        </p>

        <form @submit.prevent="submit">
            <div>
                <TextInput id="name" type="text" class="mt-1 block w-full" placeholder="Name" v-model="form.name" required autofocus autocomplete="name" />
                <InputError class="mt-2" :message="form.errors.name" />
            </div>

            <div class="mt-4">
                <TextInput id="email" type="email" class="mt-1 block w-full" placeholder="Email" v-model="form.email" required autocomplete="username" />
                <InputError class="mt-2" :message="form.errors.email" />
            </div>

            <div class="mt-4">
                <TextInput id="password" type="password" class="mt-1 block w-full" placeholder=" Password" v-model="form.password" required autocomplete="new-password" />
                <InputError class="mt-2" :message="form.errors.password" />
            </div>

            <div class="mt-4">
                <TextInput id="password_confirmation" type="password" class="mt-1 block w-full" placeholder="Confirm Password" v-model="form.password_confirmation" required autocomplete="new-password" />
                <InputError class="mt-2" :message="form.errors.password_confirmation" />
            </div>

            <AuthButton class="mt-6" :class="{ 'opacity-25': form.processing }" :disabled="form.processing">
                Continue
            </AuthButton>
            <div class="flex items-center justify-end mt-4">
                
            </div>
        </form>
    </FrontLayout>
</template>
