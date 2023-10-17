<template>
  <div>
    <header>
      <nav>
        <div class="wrapper">
          <RouterLink to="/" v-if="authenticated">View Post</RouterLink>
          <RouterLink to="/login" @click="handleLogout">
            {{ isLoggedIn ? 'Logout' : 'Login' }}
          </RouterLink>
          <RouterLink to="/register" v-if="!authenticated" :disabled="authenticated">
            Register
          </RouterLink>
        </div>
      </nav>
    </header>

    <RouterView />
  </div>
</template>

<script setup>
import { computed, ref } from 'vue'
import { RouterLink, useRouter } from 'vue-router'
import { onBeforeMount } from 'vue'

const router = useRouter()

const authenticated = computed(() => {
  const user = JSON.parse(localStorage.getItem('user'))
  console.log('user', user)
  return user !== null
})

const isLoggedIn = ref(authenticated.value)
console.log('value', isLoggedIn)

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
header {
  line-height: 1.5;
  max-height: 100vh;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: rgb(0, 102, 255);
  text-decoration: none;
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
  text-decoration: none;
}

nav a:first-of-type {
  border: 0;
  color: var(--vt-c-white);
  text-decoration: none;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
