<script>
    import Checkbox from '@/Components/Checkbox.vue';
    import GuestLayout from '@/Layouts/GuestLayout.vue';
    import InputError from '@/Components/InputError.vue';
    import InputLabel from '@/Components/InputLabel.vue';
    import { Head, Link, useForm } from '@inertiajs/vue3';
    import PrimaryButton from '@/Components/PrimaryButton.vue';
    import Input from '@/Components/Input.vue';

    export default{
        components: {
            Checkbox,
            GuestLayout,
            InputError,
            InputLabel,
            Head,
            Link,
            PrimaryButton,
            Input
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
        <Head title="Connexion"/>

        <div class="bg-white p-4 rounded-md max-w-full w-[500px]">
            <div v-if="status">
                {{ status }}
            </div>

            <form 
                @submit.prevent="submit"
                class="flex flex-col gap-4"
            >
                <div class="flex flex-col gap-2">
                    <InputLabel for="email" value="Email"/>
                    
                    <Input
                        placeholder="Email ..."
                        required
                        v-model="form.email"
                        type="email"
                        id="email"
                    />

                    <InputError :message="form.errors.email"/>
                </div>

                <div class="flex flex-col gap-2">
                    <InputLabel for="password" value="Mot de passe"/>

                    <Input
                        placeholder="Mot de passe ..."
                        required
                        v-model="form.password"
                        type="password"
                        id="password"
                    />

                    <InputError :message="form.errors.password" />
                </div>

                <div>
                    <label class="flex items-center gap-2">
                        <Checkbox name="remember" v-model:checked="form.remember" />
                        <span>Se souvenir de moi</span>
                    </label>
                </div>

                <div
                    class="flex justify-between items-center flex-wrap"
                >
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
        </div>
    </GuestLayout>
</template>
