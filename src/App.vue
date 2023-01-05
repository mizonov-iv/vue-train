<template>
  <div class="container">
    <h1>Список постов</h1>
    <input class="search__input" type="text" v-model="searchQuery" placeholder="Поиск по названию">
    <div style="display: flex; justify-content: space-between">
      <button class="btn" @click="showDialog">Создать пост</button>
      <SortDropdown
          v-model="selectedSort"
          :options="sortOptions"
      />
    </div>
    <Modal :show="dialogVisible" @hideDialog="hideDialog">
      <PostForm @createPost="createPost"/>
    </Modal>
    <PostList :posts="sortedAndSearchedPosts" @deletePost="deletePost" v-if="!isLoading"/>
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
    ],
    searchQuery: '',
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
  },
  computed: {
    sortedPosts() {
      return [...this.posts].sort((post1, post2) => post1[this.selectedSort]?.localeCompare(post2[this.selectedSort]))
    },
    sortedAndSearchedPosts () {
      return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
    }
  },
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
.search__input {
  width: 100%;
  padding: 5px;
  margin-top: 0.5rem;
  margin-bottom: 1rem;
}

</style>
