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
        v-model="descr"
    >
    <button
        class="form__btn"
        @click.prevent="createPost"
        :disabled="!title || !descr"
    >
      Создать
    </button>
  </form>
</template>

<script>
export default {
  data: () => ({
    title: '',
    descr: ''
  }),
  methods: {
    createPost() {
      const newPost = {
        id: new Date(),
        title: this.title,
        descr: this.descr
      }
      this.$emit('createPost', newPost)
      console.log(newPost)
      this.title = ''
      this.descr = ''
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