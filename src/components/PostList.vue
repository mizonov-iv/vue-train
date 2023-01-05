<template>
  <div>
    <transition-group name="list">
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
    </transition-group>


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
.list-item {
  display: inline-block;
  margin-right: 10px;
}
.list-enter-active,
.list-leave-active {
  transition: all 0.5s ease;
}
.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}
.list-move {
  transition: transform 0.8s ease;
}
</style>