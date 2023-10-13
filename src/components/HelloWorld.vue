<template>
  <div class="blog-landing">
    <h2>Blogs</h2>
    <div v-if="blogPosts">
      <ul>
        <li v-for="post in blogPosts" :key="post.id">
          <router-link :to="'/post/' + post.id">
            <h3 @click="viewPost(post.id)">{{ post.title }}</h3>
          </router-link>
        </li>
      </ul>
    </div>
    <div v-else>Loading...</div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useRouter } from 'vue-router'

const blogPosts = ref(null)

const viewPost = (postId) => {
  const router = useRouter()
  router.push(`/post/${postId}`)
}

const fetchData = () => {
  fetch('https://jsonplaceholder.typicode.com/posts')
    .then((response) => response.json())
    .then((data) => {
      blogPosts.value = data.slice(0, 10)
    })
}
onMounted(() => {
  fetchData()
})
</script>

<style scoped>
h1 {
  font-weight: 500;
  font-size: 2.6rem;
  position: relative;
  top: -10px;
}

h3 {
  font-size: 1.2rem;
}
.blog-landing {
  max-width: 600px;
  margin: 0 auto;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  margin-bottom: 20px;
}

h3 {
  margin-bottom: 10px;
  color: #007bff;
  cursor: pointer;
}

h3:hover {
  text-decoration: underline;
}
</style>
