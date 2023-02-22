<script>
    import { Head, Link } from '@inertiajs/vue3';

    export default{
        components: {
            Head,
            Link
        },
        props: {
            canLogin: Boolean,
            canRegister: Boolean,
            laravelVersion: String,
            phpVersion: String
        }
    }
</script>

<template>
    <Head title="Bienvenue" />

    <div>
        <Link
            v-if="$page.props.auth.user"
            :href="route('dashboard')"
            >Tableau de bord</Link
        >

        <template v-else>
            <Link
                :href="route('login')"
                >Connexion</Link
            >

            <Link
                v-if="canRegister"
                :href="route('register')"
                >Inscription</Link
            >
        </template>
    </div>
</template>
