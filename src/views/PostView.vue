<template>
  <div class="post" v-if="post">
    <h1>{{ post.title }}</h1>
    <p>{{ post.body }}</p>
  </div>
  <div v-else>Loading...</div>
</template>

<script setup>
import { ref, onMounted, watch } from 'vue'
import { useRoute } from 'vue-router'

const post = ref(null)
const route = useRoute()

const fetchData = (postId) => {
  fetch(`https://jsonplaceholder.typicode.com/posts/${postId}`)
    .then((response) => response.json())
    .then((data) => {
      post.value = data
    })
}

watch(
  () => route.params.id,
  (newId) => {
    fetchData(newId)
  }
)

onMounted(() => {
  fetchData(route.params.id)
})
</script>

<style>
.post{
  position: relative;
    top: 100px;
}

h1 {
  color: #007bff;
  font-size: 1.2rem;
}
</style>
