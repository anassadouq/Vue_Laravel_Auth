<script setup>
    import { useRouter } from 'vue-router';

    const router = useRouter();

    if (!localStorage.getItem('authToken')) {
        router.push('/login');
    }
</script>

<template>
    <h1 class="bg-red-500">Home page</h1>
</template>