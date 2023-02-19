<script>
    import Checkbox from '@/Components/Checkbox.vue';
    import GuestLayout from '@/Layouts/GuestLayout.vue';
    import InputError from '@/Components/InputError.vue';
    import InputLabel from '@/Components/InputLabel.vue';
    import TextInput from '@/Components/TextInput.vue';
    import { Head, Link, useForm } from '@inertiajs/vue3';
    import PrimaryButton from '@/Components/PrimaryButton.vue';

    export default{
        components: {
            Checkbox,
            GuestLayout,
            InputError,
            InputLabel,
            Head,
            Link,
            TextInput,
            PrimaryButton
        },
        props: {
            canResetPassword: Boolean,
            status: String
        },
        methods: {
            submit(){
                this.form.post(route('login'), {
                    onFinish: () => this.form.reset('password'),
                });
            }
        },
        data(){
            return {
                form: useForm({
                    email: '',
                    password: '',
                    remember: false,
                })
            }
        }
    }

</script>

<template>
    <GuestLayout>
        <Head title="Connexion" />

        <div v-if="status">
            {{ status }}
        </div>

        <form @submit.prevent="submit">
            <div>
                <InputLabel for="email" value="Email" />

                <TextInput
                    id="email"
                    type="email"
                    v-model="form.email"
                    required
                    autofocus
                    autocomplete="username"
                />

                <InputError :message="form.errors.email" />
            </div>

            <div>
                <InputLabel for="password" value="Mot de passe" />

                <TextInput
                    id="password"
                    type="password"
                    v-model="form.password"
                    required
                    autocomplete="current-password"
                />

                <InputError :message="form.errors.password" />
            </div>

            <div>
                <label>
                    <Checkbox name="remember" v-model:checked="form.remember" />
                    <span>Se souvenir de moi</span>
                </label>
            </div>

            <div>
                <Link
                    v-if="canResetPassword"
                    :href="route('password.request')"
                >
                    Mot de passe oublié ?
                </Link>

                <PrimaryButton :class="{ 'opacity-25': form.processing }" :disabled="form.processing">
                    Connexion
                </PrimaryButton>
            </div>
        </form>
    </GuestLayout>
</template>
