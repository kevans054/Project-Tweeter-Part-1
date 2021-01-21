<template>
    <div>
        <div class="row">
            <div class="col">
                <button class="btn btn-outline-light btn-sm" @click="showComments(), display()">View Comments</button>
                <!-- <button @click="hide()">hide Comment</button> -->
            </div>
        </div>
        <div class="row">
            <div class="col">
                <div v-for="comment in comments" :key="comment.commentId">
                    <div class="alert alert-primary rounded-pill">
                        <p>"{{ comment.content }}" </p>
                        <p>Posted by: {{ comment.username }}</p>
                        <p>{{ comment.createdAt }}</p>
                        <p>{{ comment.commentId }}</p>
                                              
                        <div v-if="userId == comment.userId" :commentId="comment.commentId">
                            <update-comment :commentId="comment.commentId" :comment="comment.content"></update-comment>
                            <delete-comment></delete-comment>
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
        //  mounted: function() {
        //     this.showComments();
        // },
        methods: {
            display: function () {
                this.show = true
            },
            hide: function () {
                this.show = false
            },
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
  
                    // this.$emit('update-comment', this.tweetComment)

                }).catch((error) => {
                    console.log(error)
                })
            }
        },
    }
</script>

<style scoped>
    
</style>