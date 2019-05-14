<template>
    <div v-if="currentArticle" class="container">
        <h1>{{ currentArticle.title }}</h1>

        <p>{{ currentArticle.content }}</p>

        <nuxt-link :to="{name: 'blog'}">
            <button class="btn btn-secondary">Retour</button>
        </nuxt-link>

        <!-- Button trigger modal -->
        <button type="button" class="btn btn-primary" data-toggle="modal" data-target="#exampleModal">
            Modifier
        </button>

        <button type="button" class="btn btn-danger" @click="deleteArticle">
            Supprimer
        </button>

        <!-- Modal -->
        <div class="modal fade" id="exampleModal" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
            <div class="modal-dialog modal-dialog-centered modal-lg" role="document">
                <div class="modal-content">
                    <div class="modal-header">
                        <h5 class="modal-title" id="exampleModalLabel">Modifier l'article</h5>
                        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                            <span aria-hidden="true">&times;</span>
                        </button>
                    </div>
                    <div class="modal-body">
                        <form>
                            <div class="form-group">
                                <label for="title">Titre</label>
                                <input type="text" class="form-control" id="title" v-model="currentArticle.title">
                            </div>
                            <div class="form-group">
                                <label for="content">Contenu</label>
                                <textarea class="form-control" id="content" rows="4" v-model="currentArticle.content"></textarea>
                            </div>
                        </form>
                    </div>
                    <div class="modal-footer">
                        <button type="button" class="btn btn-secondary" data-dismiss="modal">Annuler</button>
                        <button type="button" class="btn btn-success" data-dismiss="modal" @click="editArticle">Sauvegarder</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
    import axios from "~/plugins/axios";

    export default {
        async asyncData({ params }) {
            const { data } = await axios.get(`/posts/${params.id}`);

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
                title: `${this.currentArticle.title} | Blog`,
                meta: [
                    {}
                ]
            }
        },
        methods: {
            editArticle() {
                axios.put(`/posts/${this.currentArticle.id}`, {
                    title: this.currentArticle.title,
                    content: this.currentArticle.content,
                })
            },
            deleteArticle() {
                axios.delete(`/posts/${this.currentArticle.id}`)
                    .then(response => {
                        this.$router.push({ name: 'blog'})
                    })
            }
        }
    }
</script>

<style scoped>

</style>
