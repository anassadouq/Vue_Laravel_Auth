<script setup>
import { ref, onMounted } from 'vue';
import { useRouter } from 'vue-router';

const router = useRouter();

const isAuthenticated = ref(localStorage.getItem('authToken') !== null);

onMounted(() => {
  isAuthenticated.value = localStorage.getItem('authToken') !== null;
});

const handleLogout = () => {
    localStorage.removeItem('authToken');
    isAuthenticated.value = false;
    router.push('/login');
};
</script>

<template>
    <ul class="topnav">
        <li><RouterLink to="/">Logo</RouterLink></li>
        <li><RouterLink class="active" to="/">Home</RouterLink></li>
        <li v-if="!isAuthenticated" class="right"><RouterLink to="/register">Register</RouterLink></li>
        <li v-if="!isAuthenticated" class="right"><RouterLink to="/login">Login</RouterLink></li>
        <li v-else="isAuthenticated" class="right"><button @click="handleLogout">Logout</button></li>
    </ul>
</template>

<style>
    ul.topnav {
        list-style-type: none;
        margin: 0;
        padding: 0;
        overflow: hidden;
        background-color: #333;
    }

    ul.topnav li {
        float: left;
    }

    ul.topnav li a {
        display: block;
        color: white;
        text-align: center;
        padding: 14px 16px;
        text-decoration: none;
    }

    ul.topnav li a:hover:not(.active) {
        background-color: #111;
    }

    ul.topnav li a.active {
        background-color: #04AA6D;
    }

    ul.topnav li.right {
        float: right;
    }
</style>