<template>
  <li class="posts__pagination-item" v-for="pageNumber in totalPages" :key="pageNumber">
    <button :class="{ 'current-page': pageNumber === page }" @click="changePage(pageNumber)">
      {{ pageNumber }}
    </button>
  </li>
</template>

<script>
export default {
  props: {
    totalPages: {
      type: Number,
      required: true
    },
    page: {
      type: Number,
      required: true
    }
  },

  methods: {
    changePage(pageNumber) {
      this.$emit('changePage', pageNumber)
    }
  }

}
</script>

<style scoped>
.posts__pagination-item button {
  border: 1px solid grey;
  border-radius: 5px;
  padding: 8px;
  color: #ffffff;
  background-color: #141615;
}

.current-page {
  border: 1px solid #784cbe !important;
  width: 30px;
}
</style>