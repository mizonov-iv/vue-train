<template>
  <div class="container">
    <button @click="showDialog">Создать пост</button>
    <Modal :show="dialogVisible" @hideDialog="hideDialog">
      <PostForm @createPost="createPost"/>
    </Modal>
    <PostList :posts="posts" @deletePost="deletePost"/>
  </div>
</template>

<script>
import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";
import Modal from "@/components/Modal";

export default {
  name: 'App',
  components: {PostForm, PostList, Modal},
  data: () => ({
    posts: [
      {id: 1, title: 'Название 1', descr: 'Какой-то текст'},
      {id: 2, title: 'Название 2', descr: 'Какой-то текст'},
    ],
    dialogVisible: false
  }),
  methods: {
    createPost(newPost) {
      this.posts.push(newPost)
      this.dialogVisible = false
    },
    deletePost(post) {
      this.posts = this.posts.filter(p => p.id !== post.id)
    },
    showDialog() {
      this.dialogVisible = true
    },
    hideDialog() {
      this.dialogVisible = false
    }

  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
.container {
  padding: 20px;
}

</style>
