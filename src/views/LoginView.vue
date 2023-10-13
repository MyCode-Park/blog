<template>
  <div class="container mt-5">
    <h2>Login</h2>
    <form @submit.prevent="login" class="mt-3">
      <div class="forms">
        <div class="mb-3">
          <label for="email" class="form-label">Email:</label>
          <input v-model="email" type="email" class="form-control" required />
        </div>
        <div class="mb-3">
          <label for="password" class="form-label">Password:</label>
          <input v-model="password" type="password" class="form-control" required />
        </div>
      </div>
      <button type="submit" class="btn btn-primary">Login</button>
    </form>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const email = ref('')
const password = ref('')
const router = useRouter()

const login = () => {
  const storedUser = JSON.parse(localStorage.getItem('user'))
  if (
    storedUser &&
    storedUser.email === email.value &&
    storedUser.password === password.value
  ) {
    sessionStorage.setItem('authenticated', 'true')
    router.push('/post')
    window.location.reload()
  } else {
    alert('Invalid email or password.')
  }
}
</script>

<style scoped>
.forms {
  width: 30%;
}
</style>
