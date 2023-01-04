<template>
  <div class="dialog-wrapper" v-if="show" @click="$emit('hideDialog')">
    <div @click.stop class="dialog__bg">
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    show: {
      type: Boolean,
      default: false
    }
  }
}
</script>

<style scoped>
.dialog-wrapper {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
}
.dialog__bg {
  margin: auto;
  padding: 30px 15px;
  background-color: #ffff;
  border-radius: 15px;
  min-width: 300px;
  min-height: 150px;
}
</style>