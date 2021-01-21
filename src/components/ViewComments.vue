<template>
    <div>
        <div class="row">
            <div class="col">
                    <div class="row">
                        <div class="col">
                            <div v-for="comment in comments" :key="comment.commentId"><br>
                                <div class="border"><br>
                                    <p>"{{ comment.content }}" </p>
                                    <p>Posted by: {{ comment.username }}</p>
                                    <p>{{ comment.createdAt }}</p>
                                    <p>{{ comment.commentId }}</p>      
                                    <div v-if="userId == comment.userId" :commentId="comment.commentId">
                                        <update-comment :commentId="comment.commentId" :comment="comment.content"></update-comment><br>
                                        <delete-comment></delete-comment><br>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
import cookies from 'vue-cookies'
import DeleteComment from './DeleteComment.vue'
import UpdateComment from './UpdateComment.vue'

    export default {
        name: "view-comments",
        components: {
                DeleteComment,
                UpdateComment,
        },
        props: {
            tweetId: {
                type: Number,
                required: true,
            }
        },
        data() {
            return {
                comments: [],
                show: "",
                userId: cookies.get('userId')
            }
         },
         mounted: function() {
            this.showComments();
        },
        methods: {
            showComments: function() {
                axios.request({
                    url: "https://tweeterest.ml/api/comments",
                    method: "GET",
                    headers: {
                        "Content-Type": "application/json",
                        "X-Api-Key": "p3JJq3WhdMwT98hN9PTaYDE1lr2p0qKOaLfIdjyDxiorc"
                    },
                    params: {
                        tweetId: this.tweetId
                    },
                }).then((response) => {
                    console.log(response)
                    this.comments = response.data
                    this.show = true
                    window.location.reload()
                }).catch((error) => {
                    console.log(error)
                })
            }
        },
    }
</script>

<style scoped>
    
</style>