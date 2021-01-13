<template>
    <div class="comments">
        <button @click="showComments()">View Comments</button>
        <div v-for="content in comments" :key = "content.tweetId">
            <p>{{ content }}</p>
        </div>
        <button @click="show = !show">Add Comment</button>
        <div v-if="show">
            <textarea v-model="tweetComment"></textarea><br>
            <button @click="addComment()">Submit</button>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
import cookies from 'vue-cookies'
    export default {
        name: "comment-form",
         data() {
            return {
                show: false,
                tweetComment: "",
                comments: []
            }
        },
        props: {
            tweetId: {
                type: Number,
                required: true 
            },
        },
        methods: {
            addComment: function() {
                axios.request({
                    url: "https://tweeterest.ml/api/comments",
                    method: "POST",
                    headers: {
                        "Content-Type": "application/json",
                        "X-Api-Key": "p3JJq3WhdMwT98hN9PTaYDE1lr2p0qKOaLfIdjyDxiorc"
                    }, 
                    data: {
                        loginToken: cookies.get("session"),
                        tweetId: this.tweetId,
                        content: this.tweetComment
                    },
                     
                }).then((response) => {
                    console.log(response)
                    // this.$emit('update-comment', this.tweetComment)
                    this.show = false;

                }).catch((error) => {
                    console.log(error)
                })
            },

            showComments: function() {
                axios.request({
                    url: "https://tweeterest.ml/api/comments",
                    method: "GET",
                    headers: {
                        "Content-Type": "application/json",
                        "X-Api-Key": "p3JJq3WhdMwT98hN9PTaYDE1lr2p0qKOaLfIdjyDxiorc"
                    }, 
                    data: {
                        loginToken: cookies.get("session"),
                        tweetId: this.tweetId,
                        content: this.content,
                        commentId: this.commentId
                    },
                     
                }).then((response) => {
                    console.log(response)
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