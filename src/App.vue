<template>

    <post-form
        @create="createPost"
    />
    <post-list
        :posts="posts"
    />

    
</template>
<script>
import PostForm from './components/PostForm.vue'
import PostList from './components/PostList.vue'

export default {
    components: { PostForm, PostList },

    data() {
        return {
            posts: [
                { id: 1, title: 'Elden Ring', body: 'Самая новая игра от фромов' },
                { id: 2, title: 'Dark Souls 3', body: 'Лучшая игра фромов' },
                { id: 3, title: 'Sekiro', body: 'Самая нестандартная игра из солсов' },
            ],

        }
    },
    methods: {
        createPost(post) {
            this.posts.push(post)
        }
    }
}
</script>
<style>
*,
html {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}

body {
    font-family: sans-serif;
    padding: 10px;
}
</style>