<template>
  <div>
    <header>
      <nav class="navbar navbar-expand-lg navbar-light bg-light">
        <div class="container">
          <router-link
            to="/"
            class="navbar-brand"
            v-if="authenticated"
            
            exact-active-class="active"
          >
            View Post
          </router-link>
          <button
            class="navbar-toggler"
            type="button"
            data-bs-toggle="collapse"
            data-bs-target="#navbarNav"
            aria-controls="navbarNav"
            aria-expanded="false"
            aria-label="Toggle navigation"
          >
            <span class="navbar-toggler-icon"></span>
          </button>
          <div class="collapse navbar-collapse" id="navbarNav">
            <ul class="navbar-nav ml-auto">
              <li class="nav-item" v-if="authenticated">
                <router-link to="/" class="nav-link" exact exact-active-class="active">
                  View Post
                </router-link>
              </li>
              <li class="nav-item" @click="handleLogout" v-if="isLoggedIn">
                <router-link to="/" class="nav-link" exact exact-active-class="active">
                  Logout
                </router-link>
              </li>
              <li class="nav-item" v-else>
                <router-link to="/login" class="nav-link" exact exact-active-class="active">
                  Login
                </router-link>
              </li>
              <li class="nav-item" v-if="!authenticated">
                <router-link to="/register" class="nav-link" exact exact-active-class="active">
                  Register
                </router-link>
              </li>
            </ul>
          </div>
        </div>
      </nav>
    </header>
    <div class="container mt-4">
      <router-view />
    </div>
  </div>
</template>

<script setup>
import { computed, ref } from 'vue'
import { RouterLink, useRouter } from 'vue-router'
import { onBeforeMount } from 'vue'

const router = useRouter()

const authenticated = computed(() => {
  const user = JSON.parse(localStorage.getItem('user'))
  return user !== null
})

const isLoggedIn = ref(authenticated.value)

const handleLogout = () => {
  window.location.reload()
  localStorage.removeItem('user')
  isLoggedIn.value = false
  router.push('/register')
}

onBeforeMount(() => {
  if (authenticated.value) {
    router.push('/')
  } else {
    router.push('/login')
  }
})
</script>

<style scoped>
.navbar {
  border-bottom: 2px solid;
  border-color: crimson;
  background: crimson !important;
}

.nav-item{
  font-size: 1rem;
  font-weight: 600;
  margin-right: 1rem;
}

.navbar-brand {
  display: none;
}

</style>
