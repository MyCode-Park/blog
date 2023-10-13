<template>
  <div class="container mt-5">
    <h2>Register</h2>
    <form @submit.prevent="register" class="mt-3">
      <div class="forms">
        <div class="mb-3">
          <label for="username" class="form-label">Username:</label>
          <input v-model="username" type="text" class="form-control" required />
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

const username = ref('')
const password = ref('')
const router = useRouter()

const register = () => {
  if (password.value.length < 8) {
    alert('Password must be at least 8 characters long.')
    return
  }
  localStorage.setItem(
    'user',
    JSON.stringify({ username: username.value, password: password.value })
  )
  router.push('/login')
}
</script>

<style scope>
.forms {
  width: 30%;
}
</style>
