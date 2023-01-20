<template>
    <li 
        class="posts__pagination-item" 
        v-for="pageNumber in totalPages" 
        :key="pageNumber"
    >
        <button 
            :class="{ 'current-page': pageNumber === page }" 
            @click="changePage(pageNumber)"
        >
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
.posts__pagination-item button{
    padding: 8px;
}

.current-page {
    border: 2px solid #000;
    background-color: #fff;
}
</style>