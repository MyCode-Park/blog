<template>
  <div class="login-page">
    <div class="form">
      <h1 class="header">Sign In to continue</h1>
      <form @submit.prevent="login" class="login-form">
        <input v-model="email" type="email" class="form-control" required placeholder="Email ID" />
        <input
          v-model="password"
          type="password"
          class="form-control"
          required
          placeholder="Password"
          style="outline: none"
        />
        <button class="button" type="submit" :disabled="loading">
          {{ loading ? 'Invalid email or password' : 'Sign In' }}
        </button>
        <p class="message">
          Not registered?
          <router-link to="/register" class="nav-link">Create an account</router-link>
        </p>
      </form>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const email = ref('')
const password = ref('')
const router = useRouter()
const loading = ref(false)

const login = () => {
  const storedUser = JSON.parse(localStorage.getItem('user'))

  if (storedUser && storedUser.email === email.value && storedUser.password === password.value) {
    loading.value = true
    sessionStorage.setItem('authenticated', 'true')
    setTimeout(() => {
      router.push('/post')
      window.location.reload()
    })
  } else {
    loading.value = true
    setTimeout(() => {
      loading.value = false
    }, 5000)
  }
}
</script>

<style scoped>
.button {
  background: white !important;
  color: crimson !important;
  border: 1px solid !important;
  transition:
    background 0.5s ease,
    color 0.5s ease; 
}

.button:hover {
  background: crimson !important;
  color: white !important;
}

@import url(https://fonts.googleapis.com/css?family=Roboto:300);

.login-page {
  width: 360px;
  padding: 8% 0 0;
  margin: auto;
}

.header {
  display: flex;
  margin-bottom: 30px;
  font-size: 1.5rem;
  color: #000000 !important;
}
.form {
  position: relative;
  z-index: 1;
  background: #ffffff;
  max-width: 360px;
  margin: 0 auto 100px;
  padding: 45px;
  text-align: center;
  box-shadow:
    0 0 20px 0 rgba(0, 0, 0, 0.2),
    0 5px 5px 0 rgba(0, 0, 0, 0.24);
}
.form input {
  font-family: 'Roboto', sans-serif;
  outline: 0;
  background: #f2f2f2;
  width: 100%;
  border: 0;
  margin: 0 0 15px;
  padding: 15px;
  box-sizing: border-box;
  font-size: 14px;
}
.form p {
  display: flex;
  justify-content: center;
}
.form button {
  font-family: 'Roboto', sans-serif;
  text-transform: uppercase;
  outline: 0;
  width: 100%;
  border: 0;
  padding: 15px;
  color: #ffffff;
  font-size: 14px;
  -webkit-transition: all 0.3 ease;
  transition: all 0.3 ease;
  cursor: pointer;
}
.form button:hover,
.form button:active,
.form button:focus {
  background: #43a047;
}
.form input:focus {
  border: 0;
}
.form .message {
  margin: 15px 0 0;
  color: #b3b3b3;
  font-size: 12px;
}
.form .message a {
  color: crimson;
  text-decoration: none;
}
.form .register-form {
  display: none;
}
.container {
  position: relative;
  z-index: 1;
  max-width: 300px;
  margin: 0 auto;
}
.container:before,
.container:after {
  content: '';
  display: block;
  clear: both;
}
.container .info {
  margin: 50px auto;
  text-align: center;
}
.container .info h1 {
  margin: 0 0 15px;
  padding: 0;
  font-size: 36px;
  font-weight: 300;
  color: #1a1a1a;
}
.container .info span {
  color: #4d4d4d;
  font-size: 12px;
}
.container .info span a {
  color: #000000;
  text-decoration: none;
}
.container .info span .fa {
  color: #ef3b3a;
}
body {
  background: #76b852; 
  background: rgb(141, 194, 111);
  background: linear-gradient(90deg, rgba(141, 194, 111, 1) 0%, rgba(118, 184, 82, 1) 50%);
  font-family: 'Roboto', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
