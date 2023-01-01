<template>
    <div>
        <button class="button">
            <slot></slot>
        </button>
    </div>
</template>

<script>
    export default {
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