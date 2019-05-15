<template>

    <div>
        <header class="masthead">
            <div class="overlay"></div>
            <div class="container">
                <div class="row">
                    <div class="col-lg-8 col-md-10 mx-auto">
                        <div class="page-heading">
                            <h1>Les articles</h1>
                        </div>
                    </div>
                </div>
            </div>
        </header>

        <div class="container">
            <div class="row">
                <div class="col-lg-8 col-md-10 mx-auto">
                    <h2>
                        <b-button v-b-modal.articleModal>Créer un article</b-button>
                    </h2>
                    <div class="post-preview" v-for="article in articles" :key="article.id">
                        <nuxt-link :to="{name: 'blog-id', params: {id: article.id}}">
                            <h2 class="post-title">
                                {{ article.title }}
                            </h2>
                            <h3 class="post-subtitle">
                                {{ article.content  | truncate(50) }}
                            </h3>
                        </nuxt-link>
<!--                        <p class="post-meta">Posted by
                            <a href="#">Start Bootstrap</a>
                            on September 24, 2019</p>-->
                    </div>
                    <hr>
                </div>
            </div>
        </div>

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
        },
        filters: {
            truncate(string, value) {
                return string.substring(0, value) + '…';
            }
        }
    }
</script>

<style scoped>
    .masthead {
        background-image: url('../../assets/img/home-bg.jpg') !important;
    }
</style>
