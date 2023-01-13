<template>
        <button class="button">
            <slot></slot>
        </button>
</template>

<script>
    export default {
      name: 'my-button'
    }
</script>

<style scoped>
.button {
    cursor: pointer;
    border-radius: 10px;
    border: none;
    align-self: end;
    padding: 15px;
    color: white;
    background-color: black;
}
</style>