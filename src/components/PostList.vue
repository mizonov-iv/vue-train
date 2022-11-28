<template>
  <div class="post" v-for="post in posts">
    <div><strong>Название поста:</strong> {{ post.title }}</div>
    <div><strong>Текст поста:</strong> {{ post.descr }}</div>
  </div>
</template>

<script>
export default {
  props: ['posts']
}
</script>

<style scoped>
.post {
  width: 70%;
  margin: 10px auto;
  padding: 15px;
  border: 2px solid darkblue;
}
</style>