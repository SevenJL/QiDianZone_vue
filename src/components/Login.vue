<template>
    <div class="login-container">
        <h1>Login</h1>
        <form @submit.prevent="login">
            <div>
                <label for="account">Account:</label>
                <input type="text" id="account" v-model="account" required>
            </div>
            <div>
                <label for="password">Password:</label>
                <input type="password" id="password" v-model="password" required>
            </div>
            <button type="submit">Login</button>
        </form>
        <p v-if="error" class="error">{{ error }}</p>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    data() {
        return {
            account: '',
            password: '',
            error: null
        };
    },
    methods: {
        async login() {
            try {
                // axios 请求示例
                axios.post('/api/user/login', {
                    account: this.account,
                    password: this.password
                })
                    .then(response => {
                        console.log('Login successful:', response.data);
                        // 处理登录成功后的逻辑
                    })
                    .catch(error => {
                        this.error = 'Login failed. Please check your account and password.';
                        console.error(error);
                    });


            } catch (err) {
                this.error = 'Login failed. Please check your account and password.';
                console.error(err);
            }
        }
    }
};
</script>

<style>
.login-container {
    max-width: 400px;
    margin: 0 auto;
    padding: 20px;
    border: 1px solid #ccc;
    border-radius: 8px;
    background-color: #f9f9f9;
}

.error {
    color: red;
    margin-top: 10px;
}
</style>