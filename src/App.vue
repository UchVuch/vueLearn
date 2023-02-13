<template>

    <my-dialog
        v-model:show="showDialog"
    >
      <post-form
          @create="createPost"
      />
    </my-dialog>

    <h1 class="title">Страница с постами</h1>

    <div class="app">
        <my-input
            class="app__search"
            v-model:value="searchQuery"
            placeholder="Поиск..."
        />

        <div class="app__buttons">
            <my-button
                @click="openDialog"
            >
                Создать пост
            </my-button>

            <my-select
                v-model="selectedSortOption"
                :options="sortOptions"
            />
        </div>

        <post-list
            :posts="serchPosts"
            @delete="deletePost"
            v-if="!isPostsLoading"
        />
        <p v-else>
            Загрузка постов...
        </p>

        <!-- <div ref="observer" class="observer"></div> -->
        <ul class="posts__pagination">
            <PageNumberItem
                :totalPages="totalPages"
                :page="page"
                @changePage="changePageNumber"
            />
        </ul>
    </div>
</template>
<script>
import PageNumberItem from './components/PageNumberItem.vue'
import PostForm from './components/PostForm.vue'
import PostList from './components/PostList.vue'

export default {
    components: { PostForm, PostList, PageNumberItem },

    mounted() {
       this.getPosts(this.limit, this.page)
    // this.loadMorePosts(10, this.page)
    //    this.observeLoadPosts()
    },

    data() {
        return {
            posts: [
                // { id: 1, title: 'Elden Ring', body: 'Самая новая игра от фромов' },
                // { id: 2, title: 'Dark Souls 3', body: 'Лучшая игра фромов' },
                // { id: 3, title: 'Sekiro', body: 'Самая нестандартная игра из солсов' },
            ],
            showDialog: false,
            isPostsLoading: false,
            page: 1,
            limit: 10,
            totalPages: 0,
            searchQuery: '',
            selectedSortOption: '',
            sortOptions: [
                {value: 'title', name: 'По названию'},
                {value: 'body', name: 'По содержимому'},
                {value: 'id', name: 'По ID'},
            ],
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
        },
        changePageNumber(pageNumber) {
            this.page = pageNumber
        },
        async getPosts(limit, page) {
            try {
                this.isPostsLoading = true
                const response = await fetch(`https://jsonplaceholder.typicode.com/posts?_limit=${limit}&_page=${page}`)
                this.posts = await response.json()
                const headers = [...response.headers]
                let allPosts = 0
                headers.forEach(header => header[0].includes('x-total-count') ? allPosts = header[1] : null)
                this.totalPages = Math.ceil( allPosts / this.limit )
            } catch(e) {
                console.error(e)
            } finally {
                this.isPostsLoading = false
            }
        },
        async loadMorePosts(limit, page) {
            this.page += 1
            try {
                const response = await fetch(`https://jsonplaceholder.typicode.com/posts?_limit=${limit}&_page=${page}`)
                const data = await response.json()
                this.posts = [...this.posts, ...data]
                const headers = [...response.headers]
                let allPosts = 0
                headers.forEach(header => header[0].includes('x-total-count') ? allPosts = header[1] : null)
                this.totalPages = Math.ceil( allPosts / this.limit )
            } catch(e) {
                console.error(e)
            }
        },
        observeLoadPosts() {
            const options = {
                rootMargin: '0px',
                threshold: 1.0
            }
            const callback = (entries, observer) => {
                if (entries[0].isIntersecting && this.page < this.totalPages) {
                    console.log('загрузились')
                    this.loadMorePosts(10, this.page)
                }
            }
            const observer = new IntersectionObserver(callback, options)
            observer.observe(this.$refs.observer)
        }
    },

    computed: {
        sortedPosts() {
            return [...this.posts].sort((post1, post2) => {
                if (this.selectedSortOption === 'id') {
                    return post1[this.selectedSortOption] - post2[this.selectedSortOption]
                }
                return post1[this.selectedSortOption]?.localeCompare(post2[this.selectedSortOption])
            })
        },
        serchPosts() {
            return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchQuery.toLowerCase()))
        }
    },

    watch: {
        page() {
            this.getPosts(10, this.page)
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
    background-color: #1C2023;
    color: #FFFFFF;
}

.title {
    margin-bottom: 15px;
}

.app {
    max-width: 960px;
}

.app__search {
    margin-bottom: 20px;
}

.app__buttons {
    display: flex;
    align-items: center;
    justify-content: space-between;
}

.posts__pagination {
    list-style-type: none;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 10px;
    margin-top: 10px;
}

.observer {
    height: 20px;
}
</style>