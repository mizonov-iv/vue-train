<template>
  <div>
    <div class="post" v-for="post in posts" :key="post.id" v-if="$props.posts.length">
      <div>
        <div><strong>Название поста:</strong> {{ post.title }}</div>
        <div><strong>Текст поста:</strong> {{ post.body }}</div>
      </div>
      <div>
        <button class="post__btn" @click="$emit('deletePost', post)">Удалить</button>
      </div>
    </div>
    <div v-else>Посты отсутсвуют</div>
  </div>
</template>

<script>
export default {
  props: ['posts'],
}
</script>

<style scoped>
.post {
  display: flex;
  justify-content: space-between;
  align-content: center;
  width: 70%;
  margin: 10px auto;
  padding: 15px;
  border: 2px solid darkblue;
}
.post__btn {
  align-self: flex-end;
  padding: 5px 7px;
  margin-top: 0.5rem;
}
</style>