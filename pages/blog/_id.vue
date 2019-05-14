<template>
    <div v-if="currentArticle" class="container">
        <h1>{{ currentArticle.title }}</h1>

        <p>{{ currentArticle.content }}</p>

        <nuxt-link :to="{name: 'blog'}">
            <button class="btn btn-secondary">Retour</button>
        </nuxt-link>

        <!-- Button trigger modal -->
        <b-button v-b-modal.modal-edit-article variant="primary">
            Modifier
        </b-button>

        <button type="button" class="btn btn-danger" @click="deleteArticle">
            Supprimer
        </button>

        <b-modal id="modal-edit-article" title="Modifier l'article" centered size="lg">
            <form>
                <div class="form-group">
                    <label for="formTitle">Titre</label>
                    <input type="text" class="form-control" id="formTitle" v-model="currentArticle.title">
                </div>
                <div class="form-group">
                    <label for="formContent">Contenu</label>
                    <textarea class="form-control" id="formContent" rows="4" v-model="currentArticle.content"></textarea>
                </div>
            </form>
            <template slot="modal-footer">
                <b-button
                variant="secondary"
                class="float-right"
                @click="$bvModal.hide('modal-edit-article')"
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
                    .then(response => {
                        this.$bvModal.hide('modal-edit-article')
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
