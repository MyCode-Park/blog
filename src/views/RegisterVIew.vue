<template>
  <div class="container mt-5">
    <h2>Register</h2>
    <form @submit.prevent="register" class="mt-3">
      <div class="forms">
        <div class="mb-3">
          <label for="email" class="form-label">Email:</label>
          <input v-model="email" type="email" class="form-control" required />
        </div>
        <div class="mb-3">
          <label for="password" class="form-label">Password:</label>
          <input v-model="password" type="password" class="form-control" required minlength="8" />
        </div>
      </div>
      <button type="submit" class="btn btn-primary">Register</button>
    </form>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'

const email = ref('')
const password = ref('')
const router = useRouter()

const isValidEmail = (email) => {
  // Simple email validation regex
  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
  return emailRegex.test(email)
}

const register = () => {
  if (!isValidEmail(email.value)) {
    alert('Invalid email format.')
    return
  }

  if (password.value.length < 8) {
    alert('Password must be at least 8 characters long.')
    return
  }

  localStorage.setItem('user', JSON.stringify({ email: email.value, password: password.value }))
  router.push('/login')
}
</script>

<style scope>
.forms {
  width: 30%;
}
</style>
