<template>
    <div class="view-comments">
        <button @click="showComments()">View Comments</button>
            <div v-for="comment in comments" :key="comment.commentId">

                <p> {{ comment.content }}</p>
            </div> 
    </div>
</template>

<script>
import axios from 'axios'
    export default {
        name: "view-comments",
        
         data() {
            return {
                comments: [],
                display: false
            }
        },
        props: {
            tweetId: {
                type: Number,
                required: true 
            },
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
                    this.display = true;
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