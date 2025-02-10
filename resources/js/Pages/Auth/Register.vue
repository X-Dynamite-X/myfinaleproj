<script setup>
import GuestLayout from "@/Layouts/GuestLayout.vue";
import InputError from "@/Components/InputError.vue";
import InputLabel from "@/Components/InputLabel.vue";
import PrimaryButton from "@/Components/PrimaryButton.vue";
import TextInput from "@/MyComponents/FieldRequst/InputForm.vue";
import { Head, Link, useForm } from "@inertiajs/vue3";

const form = useForm({
    name: "",
    email: "",
    password: "",
    password_confirmation: "",
});

const submit = () => {
    form.post(route("register"), {
        onFinish: () => form.reset("password", "password_confirmation"),
    });
};
</script>

<template>
    <GuestLayout>
        <Head title="Register" />

        <form @submit.prevent="submit">
            <div>
                <TextInput
                    id="name"
                    type="text"
                    label="Name"
                    name="name"
                    v-model="form.name"
                    placeholder="Name"
                    :required="true"
                    :inputClass="
                        form.errors.name
                            ? 'bg-red-50 border border-red-500 text-red-900 placeholder-red-700  focus:ring-red-500 dark:bg-gray-700 focus:border-red-500  dark:text-red-500 dark:placeholder-red-500 dark:border-red-500'
                            : ''
                    "
                    autocomplete="name"
                />
                <InputError class="mt-2" :message="form.errors.name" />
            </div>

            <div class="mt-4">
                <TextInput
                    id="email"
                    type="email"
                    label="Email Address"
                    name="email"
                    v-model="form.email"
                    placeholder="Email Adresses"
                    :required="true"
                    :inputClass="
                        form.errors.email
                            ? 'bg-red-50 border border-red-500 text-red-900 placeholder-red-700  focus:ring-red-500 dark:bg-gray-700 focus:border-red-500  dark:text-red-500 dark:placeholder-red-500 dark:border-red-500'
                            : ''
                    "
                    autocomplete="email"
                />
                <InputError class="mt-2" :message="form.errors.email" />
            </div>

            <div class="mt-4">
                <TextInput
                    id="password"
                    type="password"
                    label="Password"
                    placeholder="Password"
                    name="password"
                    :required="true"
                    :inputClass="
                        form.errors.password
                            ? 'bg-red-50 border border-red-500 text-red-900 placeholder-red-700  focus:ring-red-500 dark:bg-gray-700 focus:border-red-500  dark:text-red-500 dark:placeholder-red-500 dark:border-red-500'
                            : ''
                    "
                    v-model="form.password"
                    autocomplete="password"
                />
                <InputError class="mt-2" :message="form.errors.password" />
            </div>

            <div class="mt-4">
                <TextInput
                    id="password_confirmation"
                    type="password"
                    label="Confirm Password"
                    placeholder="Confirm Password"
                    name="password_confirmation"
                    :required="true"
                    :inputClass="
                        form.errors.password_confirmation
                            ? 'bg-red-50 border border-red-500 text-red-900 placeholder-red-700  focus:ring-red-500 dark:bg-gray-700 focus:border-red-500  dark:text-red-500 dark:placeholder-red-500 dark:border-red-500'
                            : ''
                    "
                    v-model="form.password_confirmation"
                    autocomplete="new-password"
                />

                <InputError
                    class="mt-2"
                    :message="form.errors.password_confirmation"
                />
            </div>

            <div class="mt-4 flex items-center justify-end">
                <Link
                    :href="route('login')"
                    class="rounded-md text-sm text-gray-600 underline hover:text-gray-900 focus:outline-none focus:ring-2 focus:ring-indigo-500 focus:ring-offset-2 dark:text-gray-400 dark:hover:text-gray-100 dark:focus:ring-offset-gray-800"
                >
                    Already registered?
                </Link>

                <PrimaryButton
                    class="ms-4"
                    :class="{ 'opacity-25': form.processing }"
                    :disabled="form.processing"
                >
                    Register
                </PrimaryButton>
            </div>
        </form>
    </GuestLayout>
</template>
