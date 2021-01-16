<template>
    <div class="view-comments">
        <button @click="showComments()">View Comments</button>
            <div v-for="content in comments" :key = "content.tweetId">
                <p>{{ comments.content.tweetId }}</p>
            </div> 
        <!-- </div> -->
       <!-- <button @click="addComment">Add Comment</button> -->
       
    </div>
</template>

<script>
import axios from 'axios'
// import cookies from 'vue-cookies'
    export default {
        name: "view-comments",
        
         data() {
             
            return {
                // tweetComment: "",
                comments: [],
                display: false
                
            }
        },
        props: {
            tweetid: {
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
                    data: {
                        tweetId: this.tweetid
                        
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