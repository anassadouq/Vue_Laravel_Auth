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
    <nav class="bg-gray-800 text-white shadow-lg">
        <div class="container mx-auto flex justify-between items-center px-4 py-3">
            <div>
                <RouterLink to="/" class="text-xl font-bold hover:text-gray-300">Logo</RouterLink>
            </div>
        
            <ul class="flex items-center space-x-6">
                <li>
                    <RouterLink to="/" class="hover:text-gray-300 {{ $route.path === '/' ? 'text-blue-400' : '' }}">Home</RouterLink>
                </li>
  
                <li v-if="!isAuthenticated">
                    <RouterLink to="/login" class="hover:text-gray-300 {{ $route.path === '/login' ? 'text-blue-400' : '' }}">Login</RouterLink>
                </li>

                <li v-if="!isAuthenticated">
                    <RouterLink to="/register" class="hover:text-gray-300 {{ $route.path === '/register' ? 'text-blue-400' : '' }}">Register</RouterLink>
                </li>
          
                <li v-else>
                    <button @click="handleLogout" class="bg-blue-500 text-white font-medium py-1 px-4 rounded-lg hover:bg-blue-600 transition duration-200">
                        Logout
                    </button>
                </li>
            </ul>
        </div>
    </nav>
</template>