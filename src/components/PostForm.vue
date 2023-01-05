<template>
  <form class="form">
    <h5>Создать пост</h5>
    <input
        type="text"
        placeholder="Название"
        class="form__input"
        v-model="title"
    >
    <input
        type="text"
        placeholder="Описание"
        class="form__input"
        v-model="body"
    >
    <button
        class="form__btn"
        @click="createPost"
        :disabled="!title || !body"
    >
      Создать
    </button>
  </form>
</template>

<script>
export default {
  data: () => ({
    title: '',
    body: ''
  }),
  methods: {
    createPost() {
      const newPost = {
        id: new Date(),
        title: this.title,
        body: this.body
      }
      this.$emit('createPost', newPost)
      this.title = ''
      this.body = ''
    }
  }

}
</script>

<style scoped>

.form {
  width: 70%;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
}
.form__input {
  width: 100%;
  padding: 5px;
  margin-top: 0.5rem;
}
.form__btn {
  align-self: flex-end;
  padding: 5px 7px;
  margin-top: 0.5rem;
}
</style>