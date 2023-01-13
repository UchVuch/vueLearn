<template>
  <div class="dialog" v-show="show" @click="hideDialog">
    <div class="dialog__content" @click.stop>
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: 'my-dialog',
  props: {
    show: {
      type: Boolean,
      default: false
    }
  },
    methods: {
      hideDialog() {
          this.$emit('update:show', false)
      }
    }
}
</script>

<style scoped>
.dialog {
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: rgba(0,0,0, 0.6);
}

.dialog__content {
    border-radius: 10px;
    min-width: 400px;
    background-color: #fff;
    padding: 15px;
}
</style>