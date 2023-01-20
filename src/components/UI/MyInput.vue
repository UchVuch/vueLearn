<template>
  <input :value="value" @input="updateInput" class="input" type="text">
</template>

<script>
export default {
  name: 'my-input',
  props: {
    value: {
      type: [String, Number]
    }
  },
  methods: {
    updateInput(event) {
      this.$emit('update:value', event.target.value)
    }
  }
}
</script>

<style coped>
.input {
    width: 100%;
  font-size: 16px;
  border-radius: 10px;
  border: 1px solid grey;
  padding: 15px;
}

.input::placeholder {
  font-family: sans-serif;
  font-size: 16px;
}
</style>