<template>
    <div class="container">
        <h2>{{ title }}</h2>
        <ul>
            <li v-for="article in articles" :key="article.id">
                <nuxt-link :to="{name: 'blog-id', params: {id: article.id}}">
                    {{ article.name }}
                </nuxt-link>
            </li>
        </ul>
    </div>
</template>

<script>
    import axios from "~/plugins/axios";

    export default {
        async asyncData() {
            const { data } = await axios.get('/servers');
            return {
                articles: data
            }
        },

        data() {
            return {
                title: "Mes articles",
                articles: []
            }
        }
    }
</script>

<style scoped>
    .container {
        width: 980px;
        margin: 0 auto;
    }
</style>
