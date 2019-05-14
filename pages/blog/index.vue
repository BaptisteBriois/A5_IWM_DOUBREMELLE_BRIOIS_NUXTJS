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

        <!-- Button trigger modal -->
        <button type="button" class="btn btn-primary" data-toggle="modal" data-target="#exampleModalCenter">
            Launch demo modal
        </button>

        <!-- Modal -->
        <div class="modal fade" id="exampleModalCenter" tabindex="-1" role="dialog" aria-labelledby="exampleModalCenterTitle" aria-hidden="true">
            <div class="modal-dialog modal-dialog-centered" role="document">
                <div class="modal-content">
                    <div class="modal-header">
                        <h5 class="modal-title" id="exampleModalLongTitle">Modal title</h5>
                        <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                            <span aria-hidden="true">&times;</span>
                        </button>
                    </div>
                    <div class="modal-body">
                        ...
                    </div>
                    <div class="modal-footer">
                        <button type="button" class="btn btn-secondary" data-dismiss="modal">Close</button>
                        <button type="button" class="btn btn-primary">Save changes</button>
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
