<template>
    <div class="posts__wrapper">
        <h1 class="posts__title">Посты об играх</h1>
        <div class="posts">
            <post-item
                :post="post"
                :key="post.id"
                v-for="post in posts"
            />
        </div>
    </div>
</template>
<script>
import PostItem from './PostItem.vue'

export default {
    components: { PostItem },

    props: {
        posts: {
            type: Array,
            required: true,
        }
    }
}
</script>
<style scoped>
.posts__title {
    margin-top: 30px;
}

.posts {
    max-width: 960px;
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 30px;
    padding-top: 100px;
}
</style>