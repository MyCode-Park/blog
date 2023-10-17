<template>
  <div class="post" v-if="post">
    <h1>{{ post.title }}</h1>
    <p>{{ post.body }}</p>
    <i class="icon bi bi-arrow-left-circle-fill" @click="goBack"></i>
  </div>
  <div v-else>Loading...</div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useRoute, useRouter } from 'vue-router'
import 'bootstrap-icons/font/bootstrap-icons.css'

const post = ref(null)
const route = useRoute()
const router = useRouter()

const fetchData = (postId) => {
  fetch(`https://jsonplaceholder.typicode.com/posts/${postId}`)
    .then((response) => response.json())
    .then((data) => {
      post.value = data
    })
}

const goBack = () => {
  router.go(-1) // This will navigate back one step in the history stack
}

onMounted(() => {
  fetchData(route.params.id)
})
</script>

<style>
.post {
  position: relative;
  top: 50px;
}

h1 {
  color: crimson;
  font-size: 2rem;
}

.icon {
  font-size: 1.5rem;
  color: crimson;
  cursor: pointer;
}

p {
  color: var(--vt-c-text-dark);
  font-size: 1.2rem;
  margin-top: 2rem;

}
</style>
