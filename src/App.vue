<template>
  <div class="container">
    <PostForm @createPost="createPost"/>
    <PostList :posts="posts"/>
  </div>
</template>

<script>
import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";

export default {
  name: 'App',
  components: {PostForm, PostList},
  data: () => ({
    posts: [
      {id: 1, title: 'Название 1', descr: 'Какой-то текст'},
      {id: 2, title: 'Название 2', descr: 'Какой-то текст'},
    ],
  }),
  methods: {
    createPost(newPost) {
      this.posts.push(newPost)
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
