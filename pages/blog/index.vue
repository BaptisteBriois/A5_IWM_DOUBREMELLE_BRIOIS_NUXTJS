<template>
    <div class="container">
        <h2>
            {{ title }}
            <b-button v-b-modal.articleModal>Créer un article</b-button>
        </h2>

        <ul>
            <li v-for="article in articles" :key="article.id">
                <nuxt-link :to="{name: 'blog-id', params: {id: article.id}}">
                    {{ article.title }}
                </nuxt-link>
            </li>
        </ul>

        <b-modal id="articleModal" title="BootstrapVue" centered size="lg">
            <b-form-group
                id="formGroupTitle"
                label="Titre de l'article"
                label-for="formTitle"
            >
                <b-form-input
                    id="formTitle"
                    v-model="article.title"
                    type="text"
                    required
                    placeholder="Mon titre"
                ></b-form-input>
            </b-form-group>

            <b-form-group
                id="formGroupContent"
                label="Contenu de l'article"
                label-for="formContent"
            >
                <b-form-textarea
                    id="formContent"
                    v-model="article.content"
                    placeholder="Mon article"
                    rows="4"
                    max-rows="8"
                ></b-form-textarea>
            </b-form-group>

            <template slot="modal-footer">
                <b-button
                    variant="secondary"
                    class="float-right"
                    @click="$bvModal.hide('articleModal')"
                >
                    Annuler
                </b-button>
                <b-button
                    variant="success"
                    class="float-right"
                    @click="createArticle"
                >
                    Créer
                </b-button>
            </template>
        </b-modal>
    </div>
</template>

<script>
    import axios from "~/plugins/axios";

    export default {
        async asyncData() {
            const { data } = await axios.get('/posts');

            return {
                articles: data
            }
        },

        data() {
            return {
                title: "Mes articles",
                articles: [],
                article: {
                    title: "",
                    content: ""
                }
            }
        },

        head() {
            return {
                title: "Liste des articles",
                meta: [
                    {}
                ]
            }
        },

        methods: {
            createArticle() {
                axios.post("/posts", {
                    title: this.article.title,
                    content: this.article.content,
                })
                    .then(response => {
                        this.articles.push(response.data);
                        this.$bvModal.hide('articleModal')
                    })
            }
        }
    }
</script>

<style scoped>

</style>
