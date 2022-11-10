<script setup>
import FrontLayout from '@/Layouts/FrontLayout.vue';
import InputError from '@/Components/InputError.vue';
import InputLabel from '@/Components/InputLabel.vue';
import AuthButton from '@/Components/Auth/AuthButton.vue';
import TextInput from '@/Components/Auth/TextInput.vue';
import { Head, useForm } from '@inertiajs/inertia-vue3';

const props = defineProps({
    email: String,
    token: String,
});

const form = useForm({
    token: props.token,
    email: props.email,
    password: '',
    password_confirmation: '',
});

const submit = () => {
    form.post(route('password.update'), {
        onFinish: () => form.reset('password', 'password_confirmation'),
    });
};
</script>

<template>
    <FrontLayout>
        <Head title="Reset Password" />
        
        <h2 class="font-bold pt-10 text-4xl">Create new password</h2>
        <p class="text-gray-500 text-md mt-1 mb-6">Your new password must be different from previously used password.</p>

        <form @submit.prevent="submit">
            <div>
                <TextInput id="email" type="hidden" class="mt-1 block w-full" v-model="form.email" required autofocus autocomplete="username" />
                <InputError class="mt-2" :message="form.errors.email" />
            </div>

            <div class="mt-4">
                <TextInput id="password" type="password" class="mt-1 block w-full" placeholder="Password" v-model="form.password" required autocomplete="new-password" />
                <InputError class="mt-2" :message="form.errors.password" />
            </div>

            <div class="mt-4">
                <TextInput id="password_confirmation" type="password" class="mt-1 block w-full" placeholder="Confirm Password" v-model="form.password_confirmation" required autocomplete="new-password" />
                <InputError class="mt-2" :message="form.errors.password_confirmation" />
            </div>

            <div class="flex items-center justify-end mt-4">
                <AuthButton :class="{ 'opacity-25': form.processing }" :disabled="form.processing">
                    Reset Password
                </AuthButton>
            </div>
        </form>
    </FrontLayout>
</template>
