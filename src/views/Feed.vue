<template>
    <div class="container">
        <div class="row">
            <div class="col">
                <h1>Welome to the Social Network</h1>
            </div>
        </div>
        <div class="row">
            <div class="col"><br>
                <router-link class="text-dark" to="UserProfile">Checkout Your Profle Here!</router-link><br><br>
            </div>
        </div>
        <div class="container border border-dark rounded">
            <div class="row">
                <!-- <div class="row"> -->
                    <div class="col">
                        <h2 class="text-dark">Post a Tweet</h2>
                    </div>
                <!-- </div> -->
            </div>
        <!-- </div> -->
        <div class="row">
            <div class="col">
                <tweet-form></tweet-form>
            </div>
        </div>
        </div>
        <div class="row">
            <div class="col"><br>
                <div v-for="tweet in tweets" :key = "tweet.tweetId">
                    <tweet-card :tweetObject="tweet"></tweet-card>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import axios from "axios"
import TweetForm from "../components/TweetForm.vue"
import TweetCard from "../components/TweetCard.vue"


    export default {
        name: "feed-page",
        data() {
            return {
                tweets: []
            }
        },
        components: {
            TweetForm,
            TweetCard,
           
        },
        mounted: function() {
            this.getTweets();
        },
        methods: {
            reloadPage(){
                window.location.reload()
            },
            getTweets: function() {
                axios.request({
                    url: "https://tweeterest.ml/api/tweets",
                    method: "GET",
                     headers: {
                        "Content-Type": "application/json",
                        "X-Api-Key": "p3JJq3WhdMwT98hN9PTaYDE1lr2p0qKOaLfIdjyDxiorc"
                    },
                }).then((response) => {
                    console.log(response)
                    this.tweets = response.data
                }).catch((error) => {
                    console.log(error)
                })
            }
        },
       
    }
</script>

<style scoped>
   .container {
        /* background-color: rgb(20, 131, 223); */
        padding: 20px;
        margin-top: auto;
        margin-left: auto;
        margin-right: auto;
        margin-bottom: auto;
    }
</style>