<template>
    <div class="container border">
        <div class="row">
            <div class="col"><br>
                <h5>Post A Comment</h5>
            </div>
        </div>
        <div class="row"><br>
            <textarea class="col" v-model="tweetComment"></textarea>
        </div>
        <div class="row">
            <div class="col"><br>
                <button type="submit" class="btn btn-outline-light btn-sm" @click="postComment()">Post Comment</button><br><br>
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
                    window.location.reload()
                }).catch((error) => {
                    console.log(error)
                })
            }
        }
    }
    
</script>

<style scoped>
  .Mybutton{
        align-items: center;
        background-color: rgb(11, 111, 241);
        border-color: darkmagenta;
        border-width: thick;
    }
</style>