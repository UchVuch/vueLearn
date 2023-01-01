<template>
    <div class="post">
        <div>
            <h3 class="post__title"><strong>Название:</strong> {{ post.title }}</h3>
            <div class="post__body"><strong>Описание:</strong> {{ post.body }}</div>
        </div>
        <div class="post__buttons">
            <MyButton class="post__button-delete"
                @click="deletePost"
            >
                Удалить
            </MyButton>
        </div>
    </div>
</template>
<script>
import MyButton from './UI/MyButton.vue';

export default {
    components: { MyButton },
    props: {
        post: {
            type: Object,
            required: true,
        }
    },
    methods: {
        deletePost() {

        }
    },
}
</script>
<style scoped>
.post {
    display: flex;
    flex-direction: column;
}

.post__title {
    margin-bottom: 10px;
}

.post__body {
    flex-grow: 1;
    border: 1px solid grey;
    padding: 10px;
}
.post__button-delete{
    align-self: end;
    margin-top: 5px;
}
</style>