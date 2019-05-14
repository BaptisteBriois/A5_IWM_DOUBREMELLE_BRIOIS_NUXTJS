<template>
    <div class="container">
        <h2>
            {{ title }}
            <button type="button" class="btn btn-primary" data-toggle="modal" data-target="#createModal">
                Créer un article
            </button>
        </h2>
        <ul>
            <li v-for="article in articles" :key="article.id">
                <nuxt-link :to="{name: 'blog-id', params: {id: article.id}}">
                    {{ article.title }}
                </nuxt-link>
            </li>
        </ul>

        <!-- Modal -->
        <div class="modal fade" id="createModal" tabindex="-1" role="dialog" aria-labelledby="createModalLabel" aria-hidden="true">
            <div class="modal-dialog modal-lg modal-dialog-centered" role="document">
                <div class="modal-content">
                    <div class="modal-header">
                        <h5 class="modal-title" id="modalLabel">Création d'un article</h5>
                        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                            <span aria-hidden="true">&times;</span>
                        </button>
                    </div>
                    <div class="modal-body">
                        <form>
                            <div class="form-group">
                                <label for="title">Titre</label>
                                <input type="text" class="form-control" id="title" name="title" placeholder="Mon titre" v-model="article.title">
                            </div>
                            <div class="form-group">
                                <label for="content">Contenu de l'article</label>
                                <textarea rows="8" class="form-control" id="content" name="content" placeholder="Mon article" v-model="article.content"></textarea>
                            </div>
                        </form>
                    </div>
                    <div class="modal-footer">
                        <button type="button" class="btn btn-secondary" data-dismiss="modal">Annuler</button>
                        <button type="button" class="btn btn-success" data-dismiss="modal" @click="createArticle">Créer</button>
                    </div>
                </div>
            </div>
        </div>
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
