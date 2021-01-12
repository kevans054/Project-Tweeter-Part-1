<template>
    <div id="feed-title">
        <div id="login-logo">
        <img src="../assets/twitterlogo.png" alt="Twitter logo">
    </div>
        <h1>My Tweeter Feed</h1>
        
        <button @click="getTweets">Refresh Tweets</button>
        <div class="feed-container" v-for="tweet in tweets" :key = "tweet.tweetId">
            <tweet-card :tweetObject="tweet"></tweet-card>
        </div>
        <div>
            <h1>Post a tweet</h1>
            <tweet-form></tweet-form>
        </div>
    </div>
</template>

<script>
import axios from "axios"
import TweetForm from "../components/TweetForm.vue"
import TweetCard from "../components/Tweet.vue"

    export default {
        name: "feed-page",
        data() {
            return {
                tweets: []
            }
        },
        components: {
            TweetForm,
            TweetCard
        },
        mounted: function() {
            this.getTweets();
        },
        methods: {
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
    .feed-container{
        display: grid;

    }
</style>