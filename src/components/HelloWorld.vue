<template>
  <div class="blog-landing">
    <h2>Blogs</h2>
    <div v-if="blogPosts">
      <ul>
        <li v-for="post in blogPosts" :key="post.id">
          <router-link :to="'/post/' + post.id">
            <h3 @click="viewPost(post.id)" class="title">{{ post.title }}</h3>
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
.title {
  text-decoration: underline;
  color: crimson;
  text-decoration-color: white;
  transition: transform 0.3s ease;
  font-size: 1.3rem;
}

.title:hover {
  transform: scale(1.1);
  text-decoration: underline;
  text-decoration-color: white; 
}

h2 {
  color: var(--vt-c-white) !important;
  margin: 2rem 0;
}

h3 {
  font-size: 1.2rem;
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
  cursor: pointer;
  text-decoration: none;
}

h3:hover {
  text-decoration: underline;
}
</style>
