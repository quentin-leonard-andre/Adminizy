<script>
    import GuestLayout from '@/Layouts/GuestLayout.vue';
    import InputError from '@/Components/InputError.vue';
    import InputLabel from '@/Components/InputLabel.vue';
    import PrimaryButton from '@/Components/PrimaryButton.vue';
    import TextInput from '@/Components/TextInput.vue';
    import { Head, Link, useForm } from '@inertiajs/vue3';

    export default{
        components: {
            GuestLayout,
            InputError,
            InputLabel,
            PrimaryButton,
            TextInput,
            Head,
            Link,
            useForm
        },
        data(){
            return{
                form: useForm({
                    name: '',
                    email: '',
                    password: '',
                    password_confirmation: '',
                    terms: false,
                })
            };
        },
        methods: {
            submit(){
                this.form.post(route('register'), {
                    onFinish: () => this.form.reset('password', 'password_confirmation'),
                });
            }
        }
    }
</script>

<template>
    <GuestLayout>
        <Head title="Inscription" />

        <form @submit.prevent="submit">
            <div>
                <InputLabel for="name" value="Nom" />

                <TextInput
                    id="name"
                    type="text"
                    v-model="form.name"
                    required
                    autofocus
                    autocomplete="name"
                />

                <InputError :message="form.errors.name" />
            </div>

            <div>
                <InputLabel for="email" value="Email" />

                <TextInput
                    id="email"
                    type="email"
                    v-model="form.email"
                    required
                    autocomplete="username"
                />

                <InputError :message="form.errors.email" />
            </div>

            <div class="mt-4">
                <InputLabel for="password" value="Mot de passe" />

                <TextInput
                    id="password"
                    type="password"
                    v-model="form.password"
                    required
                    autocomplete="new-password"
                />

                <InputError :message="form.errors.password" />
            </div>

            <div class="mt-4">
                <InputLabel for="password_confirmation" value="Confirmer le mot de passe" />

                <TextInput
                    id="password_confirmation"
                    type="password"
                    v-model="form.password_confirmation"
                    required
                    autocomplete="new-password"
                />

                <InputError :message="form.errors.password_confirmation" />
            </div>

            <div class="flex items-center justify-end mt-4">
                <Link
                    :href="route('login')"
                >
                    Déjà enregistré ?
                </Link>

                <PrimaryButton :class="{ 'opacity-25': form.processing }" :disabled="form.processing">
                    Inscription
                </PrimaryButton>
            </div>
        </form>
    </GuestLayout>
</template>
