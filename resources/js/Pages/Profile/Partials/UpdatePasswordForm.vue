<script setup>
import InputError from "@/Components/InputError.vue";
import InputLabel from "@/Components/InputLabel.vue";
import PrimaryButton from "@/Components/PrimaryButton.vue";
import TextInput from "@/MyComponents/FieldRequst/InputForm.vue";
import { useForm } from "@inertiajs/vue3";
import { ref } from "vue";

const passwordInput = ref(null);
const currentPasswordInput = ref(null);

const form = useForm({
    current_password: "",
    password: "",
    password_confirmation: "",
});

const updatePassword = () => {
    form.put(route("password.update"), {
        preserveScroll: true,
        onSuccess: () => {
            form.reset();
        },
        onError: () => {
            if (form.errors.password) {
                form.reset("password", "password_confirmation");
            }
            if (form.errors.current_password) {
                form.reset("current_password");
            }
        },
    });
};
</script>

<template>
    <section>
        <header>
            <h2 class="text-lg font-medium text-gray-900 dark:text-gray-100">
                Update Password
            </h2>

            <p class="mt-1 text-sm text-gray-600 dark:text-gray-400">
                Ensure your account is using a long, random password to stay
                secure.
            </p>
        </header>

        <form @submit.prevent="updatePassword" class="mt-6 space-y-6">
            <div>
                <TextInput
                    id="current_password"
                    ref="currentPasswordInput"
                    v-model="form.current_password"
                    type="password"
                    label="Current Password"
                    placeholder="Current Password"
                    name="current_password"
                    :required="true"
                    :errorMessage2="form.errors.current_password"
                    :inputClass="
                        form.errors.current_password
                            ? 'bg-red-50 border border-red-500 text-red-900 placeholder-red-700  focus:ring-red-500 dark:bg-gray-700 focus:border-red-500  dark:text-red-500 dark:placeholder-red-500 dark:border-red-500'
                            : ''
                    "
                    autofocus
                    autocomplete="current-password"
                />
            </div>

            <div>
                <TextInput
                    id="password"
                    type="password"
                    ref="passwordinput"
                    label="New Password"
                    placeholder="New Password"
                    name="password"
                    :required="true"
                    :inputClass="
                        form.errors.password
                            ? 'bg-red-50 border border-red-500 text-red-900 placeholder-red-700  focus:ring-red-500 dark:bg-gray-700 focus:border-red-500  dark:text-red-500 dark:placeholder-red-500 dark:border-red-500'
                            : ''
                    "
                    autofocus
                    :errorMessage2="form.errors.password"
                    v-model="form.password"
                    autocomplete="new-password"
                />
            </div>

            <div>
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
                    :errorMessage2="form.errors.password_confirmation"
                    autofocus
                    autocomplete="new-password"
                />
            </div>

            <div class="flex items-center gap-4">
                <PrimaryButton :disabled="form.processing">Save</PrimaryButton>

                <Transition
                    enter-active-class="transition ease-in-out"
                    enter-from-class="opacity-0"
                    leave-active-class="transition ease-in-out"
                    leave-to-class="opacity-0"
                >
                    <p
                        v-if="form.recentlySuccessful"
                        class="text-sm text-gray-600 dark:text-gray-400"
                    >
                        Saved.
                    </p>
                </Transition>
            </div>
        </form>
    </section>
</template>
