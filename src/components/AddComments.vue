<template>
    <div class="create-comment">
        <h3>Add Comments</h3>
        <div>
             <div>
            <textarea v-model="tweetComment"></textarea><br>
            <button @click="postComment()">Submit</button>
        </div>
        </div>
    </div>
</template>

<script>
import cookies from 'vue-cookies'
import axios from "axios"
    export default {
        name: "add-comments",

        data() {
             
            return {
                comments: [],
                tweetComment: "",
            }
        },
        props: {
            tweetid: {
                type: Number,
                required: true 
            },
        },
        methods: {
            postComment: function() {
                
                axios.request({
                    url: "https://tweeterest.ml/api/comments",
                    method: "POST",
                    headers: {
                        "Content-Type": "application/json",
                        "X-Api-Key": "p3JJq3WhdMwT98hN9PTaYDE1lr2p0qKOaLfIdjyDxiorc"
                    }, 
                    data: {
                        loginToken: cookies.get("session"),
                        tweetId: this.tweetid,
                        content: this.tweetComment
                        
                    },
                     
                }).then((response) => {
                    console.log(response)
                    // this.$emit('update-comment', this.tweetComment)
                    // this.show = false;

                }).catch((error) => {
                    console.log(error)
                })
            }
        }
    }
    
</script>

<style scoped>

</style>