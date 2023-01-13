<template>
    <div>
        <form class="create-post"
        @submit.prevent>
            <h3>Создать пост</h3>
            <my-input
                class="create-post__input"
                placeholder="Название"
                v-model:value="post.title"
            />
            <textarea
                class="create-post__input"
                placeholder="Описание"
                v-model="post.body"
            >
            </textarea>
            <my-button class="create-post__button"
                @click="createPost()"
            >
                Создать
            </my-button>
        </form>
    </div>
</template>
<script>

export default {
    data() {
        return {
            post: {
                title: "",
                body: ""
            }
        };
    },
    methods: {
        createPost() {
            this.post.id = Date.now()
            this.$emit("create", this.post)
            this.post = {
                title: "",
                body: ""
            };
        }
    },
}
</script>
<style scoped>
.create-post {
    font-family: sans-serif;
    max-width: 600px;
    display: flex;
    flex-direction: column;
    gap: 15px;
}

.create-post__input {
    resize: vertical;
    font-size: 16px;
    border-radius: 10px;
    border: 1px solid grey;
    padding: 15px;
}

.create-post__input::placeholder {
    font-family: sans-serif;
    font-size: 16px;
}

.create-post__button {
    align-self: end;
}

.create-post__button:hover {
    box-shadow:0 0 20px rgb(138, 135, 135);
}
</style>