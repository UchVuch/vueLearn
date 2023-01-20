<template>
    <div
        class="posts__wrapper"
        v-if="posts.length > 0"
    >
        <h2 class="posts__title">Посты об играх</h2>
        <div class="posts">
            <transition-group name="user-list">
                <post-item
                    :post="post"
                    :key="post.id"
                    v-for="post in posts"
                    @delete="$emit('delete', post)"
                />
            </transition-group>
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

.user-list-item {
    display: inline-block;
    margin-right: 10px;
}

.user-list-enter-active,
.user-list-leave-active {
    transition: all .4s ease;
}

.user-list-enter-from,
.user-list-leave-to {
    opacity: 0;
    transform: translateY(30px);
}

.user-list-move {
    transition: transform 0.8s ease;
}
</style>
