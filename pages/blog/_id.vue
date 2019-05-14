<template>
    <div v-if="currentArticle" class="container">
        <h1>{{ currentArticle.title }}</h1>

        <p>{{ currentArticle.content }}</p>

        <nuxt-link :to="{name: 'blog'}">
            <button class="btn btn-secondary">Retour</button>
        </nuxt-link>

        <!-- Button trigger modal -->
        <b-button variant="primary" @click="showModal">
            Modifier
        </b-button>

        <button type="button" class="btn btn-danger" @click="deleteArticle">
            Supprimer
        </button>

        <b-modal id="editArticleModal" title="Modifier l'article" centered size="lg">
            <form>
                <div class="form-group">
                    <label for="formTitle">Titre</label>
                    <input type="text" class="form-control" id="formTitle" v-model="title">
                </div>
                <div class="form-group">
                    <label for="formContent">Contenu</label>
                    <textarea class="form-control" id="formContent" rows="4" v-model="content"></textarea>
                </div>
            </form>
            <template slot="modal-footer">
                <b-button
                variant="secondary"
                class="float-right"
                @click="$bvModal.hide('editArticleModal')"
                >
                    Annuler
                </b-button>
                <b-button
                variant="success"
                class="float-right"
                @click="editArticle"
                >
                    Sauvegarder
                </b-button>
            </template>
        </b-modal>

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
                currentArticle: null,
                title: 'a',
                content: 'a'
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
            showModal() {
                this.title = this.currentArticle.title;
                this.content = this.currentArticle.content;
                this.$bvModal.show('editArticleModal')
            },
            editArticle() {
                axios.put(`/posts/${this.currentArticle.id}`, {
                    title: this.title,
                    content: this.content,
                })
                    .then(response => {
                        this.currentArticle.title = this.title;
                        this.currentArticle.content = this.content;
                        this.$bvModal.hide('editArticleModal')
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
