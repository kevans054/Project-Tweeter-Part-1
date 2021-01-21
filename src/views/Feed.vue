<template>
    <div class="container">
        <div class="row">
            <div class="col">
                <h1 class="text-info">Welome to your Social Network</h1>
            </div>
        </div>
        <div class="container border border-dark rounded">
            <div class="row">
            <div class="col">
                <button class="btn btn-outline-dark btn-sm" @click="show = !show">View Your Profile Here</button>
                            <div v-if="show">
                                <view-profile :userId="userId"></view-profile>
                            </div>
            </div>
        </div>
            <div class="row">
                    <div class="col"><br>
                        <h2 class="text-dark">Post a Tweet</h2>
                    </div>
            </div>
            
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
import cookies from 'vue-cookies'
import TweetForm from "../components/TweetForm.vue"
import TweetCard from "../components/TweetCard.vue"
import ViewProfile from '../components/UserProfile.vue'


    export default {
        name: "feed-page",
        data() {
            return {
                tweets: [],
                userId: cookies.get('userId'),
                show: false
            }
        },
        components: {
            TweetForm,
            TweetCard,
            ViewProfile
           
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
        padding: 20px;
        margin-top: auto;
        margin-left: auto;
        margin-right: auto;
        margin-bottom: auto;
    }
</style>