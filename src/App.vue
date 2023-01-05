<template>
  <div class="container">
    <h1>Список постов</h1>
    <button class="btn" @click="showDialog">Создать пост</button>
    <SortDropdown
        v-model="selectedSort"
        :options="sortOptions"
    />
    <Modal :show="dialogVisible" @hideDialog="hideDialog">
      <PostForm @createPost="createPost"/>
    </Modal>
    <PostList :posts="posts" @deletePost="deletePost" v-if="!isLoading"/>
    <div v-else>Идет загрузка...</div>
  </div>
</template>

<script>
import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";
import Modal from "@/components/Modal";
import SortDropdown from "@/components/SortDropdown";
import axios from "axios";

export default {
  name: 'App',
  components: {PostForm, PostList, Modal, SortDropdown},
  data: () => ({
    posts: [],
    dialogVisible: false,
    isLoading: false,
    selectedSort: '',
    sortOptions: [
      {value: 'title', name: 'По заголовку'},
      {value: 'body', name: 'По содержанию'},
    ]
  }),
  methods: {
    createPost(newPost) {
      this.posts.push(newPost)
      this.dialogVisible = false
    },
    deletePost(post) {
      this.posts = this.posts.filter(p => p.id !== post.id)
    },
    fetchPosts() {
      this.isLoading = true
      axios.get('https://jsonplaceholder.typicode.com/posts?_limit=15')
          .then(response => {
            this.posts = response.data
            this.isLoading = false
          })
          .catch(error => {
            console.log(error)
          })
    },
    showDialog() {
      this.dialogVisible = true
    },
    hideDialog() {
      this.dialogVisible = false
    }
  },
  mounted() {
    this.fetchPosts()
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
.btn {
  padding: 10px;
  margin: 5px;
  background-color: blueviolet;
  border: none;
}
.btn:hover {
  color: #FFFF;
}

</style>
