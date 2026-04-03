<template>
    <!-- Main -->
    <div id="main">
        <!-- Post -->
        <template v-for="post in posts.data">
            <PostComponent :post="post" :changePage="changePage" :PUBLIC="PUBLIC" :likeArray="likeArray" />
        </template>

        <!-- Pagination -->
        <!-- <ul class="actions pagination">
            <li>
                <a
                    href="#"
                    @click.prevent="postsHome(posts.current_page - 1)"
                    :class="{ disabled: posts.current_page == 1 }"
                    class="button big previous"
                    >Previous Page</a
                >
            </li>
            <li>
                <a
                    href="#"
                    @click.prevent="postsHome(posts.current_page + 1)"
                    :class="{ disabled: posts.current_page == posts.last_page }"
                    class="button big next"
                    >Next Page</a
                >
            </li>
        </ul> -->
    </div>

    <section id="sidebar">
        <!-- Intro -->
        <section id="intro">
            <header>
                <p>Фильтрация</p>
            </header>
            <div class="form-check">
                <h4>Категория</h4>
                <input class="form-check-input" type="radio" name="radioDefault" id="radioDefault1" />
                <label class="form-check-label" for="radioDefault1"> Завтрак </label>
                <input class="form-check-input" type="radio" name="radioDefault" id="radioDefault1" />
                <label class="form-check-label" for="radioDefault1"> Обед </label>
                <input class="form-check-input" type="radio" name="radioDefault" id="radioDefault1" />
                <label class="form-check-label" for="radioDefault1"> Ужин </label>
            </div>
            <div class="form-check">
                <h4>Время</h4>
                <input class="form-check-input" type="radio" name="radioDefault" id="radioDefault1" />
                <label class="form-check-label" for="radioDefault1"> до 30 мин </label>
                <input class="form-check-input" type="radio" name="radioDefault" id="radioDefault1" />
                <label class="form-check-label" for="radioDefault1"> 30-60 мин </label>
                <input class="form-check-input" type="radio" name="radioDefault" id="radioDefault1" />
                <label class="form-check-label" for="radioDefault1"> более 60 мин </label>
            </div>
            <div class="form-check">
                <h4>Сложность</h4>
                <input class="form-check-input" type="radio" name="radioDefault" id="radioDefault1" />
                <label class="form-check-label" for="radioDefault1"> Легко </label>
                <input class="form-check-input" type="radio" name="radioDefault" id="radioDefault1" />
                <label class="form-check-label" for="radioDefault1"> Средне </label>
                <input class="form-check-input" type="radio" name="radioDefault" id="radioDefault1" />
                <label class="form-check-label" for="radioDefault1"> Сложно </label>
            </div>
        </section>
    </section>
</template>
<script>
import PostComponent from '@/components/PostComponent.vue';
import SidebarComponent from '@/components/SidebarComponent.vue';

export default {
    name: 'HomePage',
    props: ['server', 'changePage', 'PUBLIC', 'user'],
    components: {
        PostComponent,
        SidebarComponent,
    },
    data() {
        return {
            posts: [],
            likeArray: [],
        };
    },
    mounted() {
        this.postsHome();
    },
    methods: {
        postsHome(page = 1) {
            this.server('postsHome/?page=' + page, 'GET', null, this.user.id)
                .then((result) => {
                    this.posts = result.posts;
                    this.likeArray = result.likeArray;
                })
                .catch((error) => console.log('error', error));
        },
    },
};
</script>
