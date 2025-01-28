<script setup>
      import Navbar from '@/components/Navbar.vue';

    import { useRouter } from 'vue-router';

    const router = useRouter();

    if (!localStorage.getItem('authToken')) {
        router.push('/login');
    }
</script>

<template>
    <Navbar/>
    <h1>Home page</h1>
</template>