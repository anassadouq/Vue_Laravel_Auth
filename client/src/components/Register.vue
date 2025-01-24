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
    <form @submit.prevent="handleSubmit">
        <div class="container">
            <h1>Register</h1>

            <label for="name"><b>Name</b></label>
            <input type="text" v-model="data.name" placeholder="Enter Name" name="name" required>

            <label for="email"><b>Email</b></label>
            <input type="text" v-model="data.email" placeholder="Enter Email" name="email" required>

            <label for="psw"><b>Password</b></label>
            <input type="password" v-model="data.password" placeholder="Enter Password" name="password" required>

            <label for="psw"><b>Password confirmation</b></label>
            <input type="password" v-model="data.password_confirmation" placeholder="Confirm Password" name="password_confirmation" required>
            
            <button type="submit" class="registerbtn">Register</button>
        </div>
        
        <div class="container signin">
            <p>Already have an account? <RouterLink to="login">Sign in</RouterLink>.</p>
        </div>
    </form>
</template>

<style>
    .container {
    padding: 16px;
    background-color: white;
    }

    /* Full-width input fields */
    input[type=text], input[type=password] {
    width: 100%;
    padding: 15px;
    margin: 5px 0 22px 0;
    display: inline-block;
    border: none;
    background: #f1f1f1;
    }

    input[type=text]:focus, input[type=password]:focus {
    background-color: #ddd;
    outline: none;
    }

    /* Overwrite default styles of hr */
    hr {
    border: 1px solid #f1f1f1;
    margin-bottom: 25px;
    }

    /* Set a style for the submit button */
    .registerbtn {
    background-color: #04AA6D;
    color: white;
    padding: 16px 20px;
    margin: 8px 0;
    border: none;
    cursor: pointer;
    width: 100%;
    opacity: 0.9;
    }

    .registerbtn:hover {
    opacity: 1;
    }

    /* Add a blue text color to links */
    a {
    color: dodgerblue;
    }

    /* Set a grey background color and center the text of the "sign in" section */
    .signin {
    background-color: #f1f1f1;
    text-align: center;
    }
</style>