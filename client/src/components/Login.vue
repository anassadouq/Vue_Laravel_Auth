<script setup>
import { ref } from 'vue';
import axios from 'axios';
import { useRouter } from 'vue-router';
import { useToast } from 'vue-toastification';
import { RouterLink } from 'vue-router';

const router = useRouter();
const toast = useToast();

const form = ref({
    email: "",
    password: ""
});

const handleLogin = async () => {
    try {
        const response = await axios.post('http://127.0.0.1:8000/api/login', {
            email: form.value.email,
            password: form.value.password
        });
        localStorage.setItem('authToken', response.data.token);
        router.push('/');
    } catch (error) {
        console.error('Error fetching user', error);
        toast.error('User was not logged');
    }
};
</script>

<template>
    <h2>Login</h2>
    <form @submit.prevent="handleLogin" method="post">
        <div class="container">
            <label for="email"><b>Email</b></label>
            <input type="text" id="email" v-model="form.email" placeholder="exemple@gmail.com" name="email" required>

            <label for="password"><b>Password</b></label>
            <div class="password-container">
                <input type='password'  v-model="form.password" placeholder="Enter Password" name="password" required/>
            </div>
                
            <button type="submit">Login</button>
            <div class="container signin">
                <p>I don't have an account? <RouterLink to="register">Sign up</RouterLink></p>
            </div>
        </div>
    </form>
</template>

<style>
    form {
        border: 3px solid #f1f1f1;
    }

    input[type=text], input[type=password] {
        width: 100%;
        padding: 12px 20px;
        margin: 8px 0;
        display: inline-block;
        border: 1px solid #ccc;
        box-sizing: border-box;
    }

    button {
        background-color: #04AA6D;
        color: white;
        padding: 14px 20px;
        margin: 8px 0;
        border: none;
        cursor: pointer;
        width: 100%;
    }

    button:hover {
        opacity: 0.8;
    }

    .container {
        padding: 16px;
    }

    .password-container {
        display: flex;
        align-items: center;
        position: relative;
    }

    .password-toggle {
        position: absolute;
        right: 12px;
        background: none;
        border: none;
        color: #04AA6D;
        cursor: pointer;
    }
</style>