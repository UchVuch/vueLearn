<template>
    <div
        class="posts__wrapper"
        v-if="posts.length > 0"
    >
        <h2 class="posts__title">Посты об играх</h2>
        <div class="posts">
            <post-item
                :post="post"
                :key="post.id"
                v-for="post in posts"
                @delete="$emit('delete', post)"
            />
        </div>
    </div>
    <h2
        class="no-posts"
        v-else
    >
      Постов нет
    </h2>
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
.no-posts {
  color: grey;
  margin-top: 20px;
}

.posts__title {
    margin-top: 30px;
}

.posts {
    max-width: 960px;
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 30px;
    padding-top: 50px;
}
</style>