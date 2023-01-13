<template>

    <my-dialog
        v-model:show="showDialog"
    >
      <post-form
          @create="createPost"
      />
    </my-dialog>

    <h1 class="title">Страница с постами</h1>
    <my-button
      @click="openDialog"
    >
      Создать пост
    </my-button>
    <post-list
        :posts="posts"
        @delete="deletePost"
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
            showDialog: false,
        }
    },
    methods: {
        createPost(post) {
            this.showDialog = false
            this.posts.push(post)
        },
        deletePost(post) {
            this.posts = this.posts.filter(p => p.id !== post.id)
        },
        openDialog() {
            this.showDialog = true
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

.title {
    margin-bottom: 15px;
}
</style>