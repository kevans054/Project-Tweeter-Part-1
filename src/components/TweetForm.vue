<template>
    <div class="container border">
        
        <div class="row">
            <div class="col">
                <h4>{{ tweetStatus }}</h4>
            </div>
        </div>
        <div class="row">
            <!-- <div> -->
                <textarea id="tweetbox" class="col" v-model="tweetContent"></textarea>
            <!-- </div> -->
        </div>
        <div class="row">
            <div class="col"><br>
                <button class="btn btn-outline-light btn-sm" @click="postTweet()">Post</button>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
import cookies from 'vue-cookies'
    export default {
        name: 'tweet-form',
        data() {
            return {
                tweetContent: "",
                tweetStatus: "tweet!"
            }
        },
        methods: {
            postTweet: function() {
                this.tweetStatus = "tweeting!"
                axios.request({
                    url: "https://tweeterest.ml/api/tweets",
                    headers: {
                        "Content-Type": "application/json",
                        "X-Api-Key": "p3JJq3WhdMwT98hN9PTaYDE1lr2p0qKOaLfIdjyDxiorc"
                    },
                    method: "POST",
                    data: {
                        loginToken: cookies.get("session"),
                        content: this.tweetContent
                    }
                }).then((response) => {
                    console.log(response)
                    this.tweetStatus = "Tweeted!"
                }).catch((error) => {
                        console.log(error)
                        this.tweetStatus = "Failed to tweet!"
                })
            }
        },
    }
</script>

<style scoped>
    .container {
         background-color: rgb(20, 131, 223);
    }

</style>