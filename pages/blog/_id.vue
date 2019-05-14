<template>
    <div v-if="currentArticle" class="container">
        <h1>{{ currentArticle.name }}</h1>

        <p>{{ currentArticle.description }}</p>

        <nuxt-link :to="{name: 'blog'}">
            <button>Retour</button>
        </nuxt-link>
    </div>
</template>

<script>
    import axios from "~/plugins/axios";

    export default {
        async asyncData({ params }) {
            const { data } = await axios.get(`/servers/${params.id}`);

            return {
                currentArticle: data
            }
        },

        data() {
            return {
                currentArticle: null
            }
        },

        head() {
            return {
                title: `${this.currentArticle.name} | Mon site internet`,
                meta: [
                    {}
                ]
            }
        },
    }
</script>

<style scoped>

</style>
