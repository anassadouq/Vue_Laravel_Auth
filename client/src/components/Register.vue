<script setup>
    import { RouterLink } from 'vue-router';
    import { reactive } from 'vue';
    import axios from 'axios';
    import router from '@/router';
    import { useToast } from 'vue-toastification';

    const data = reactive({
        name: "",
        email: "",
        password: "",
        password_confirmation:"",
    });

    const toast = useToast();

    const handleSubmit = async () => {
        const newUser = {
            name: data.name,
            email: data.email,
            password: data.password,
            password_confirmation: data.password_confirmation,
        }

        try {
            const response = await axios.post('http://127.0.0.1:8000/api/register', newUser);
            toast.success('User Added Successfully');
            router.push('/login');
        } catch (error) {
            console.error('Error fetching user', error);
            toast.error('User was not added');
        }
    }
</script>

<template>
    <div class="flex items-center justify-center min-h-screen bg-gray-100">
        <div class="w-full max-w-lg bg-white rounded-lg shadow-lg p-8">
            <h1 class="text-2xl font-bold text-center text-gray-800 mb-6">Register</h1>
            <form @submit.prevent="handleSubmit" method="post">
                <div class="mb-4">
                    <label for="name" class="block text-sm font-medium text-gray-700 mb-2">Name</label>
                    <input type="text" v-model="data.name" placeholder="Enter Name" name="name" required class="w-full px-4 py-2 border rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent"/>
                </div>
  
                <div class="mb-4">
                    <label for="email" class="block text-sm font-medium text-gray-700 mb-2">Email</label>
                    <input type="email" v-model="data.email" placeholder="Enter Email" name="email" required class="w-full px-4 py-2 border rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent"/>
                </div>
  
                <div class="mb-4">
                    <label for="psw" class="block text-sm font-medium text-gray-700 mb-2">Password</label>
                    <input type="password" v-model="data.password" placeholder="Enter Password" name="password" required class="w-full px-4 py-2 border rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent"/>
                </div>
  
                <div class="mb-4">
                    <label for="psw-confirmation" class="block text-sm font-medium text-gray-700 mb-2">Password Confirmation</label>
                    <input type="password" v-model="data.password_confirmation" placeholder="Confirm Password" name="password_confirmation" required class="w-full px-4 py-2 border rounded-lg shadow-sm focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-transparent"/>
                </div>
  
                <button type="submit" class="w-full bg-blue-500 text-white font-medium py-2 px-4 rounded-lg hover:bg-blue-600 transition duration-200">
                    Register
                </button>
            </form>
  
            <div class="text-center mt-4 text-sm text-gray-600">
                <p> Already have an account? 
                    <RouterLink to="login" class="text-blue-500 hover:underline">Sign in</RouterLink>
                </p>
            </div>
        </div>
    </div>
</template>