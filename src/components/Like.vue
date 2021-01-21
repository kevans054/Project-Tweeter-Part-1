<template>
    <div>
        <div class="row">
            <div class="col">
            </div>
            <div class="col">
            </div>
            <div class="col"><br>
                <button class="btn btn-outline-light btn-sm" @click="likeTweet()" v-if="likes == false">like this tweet</button>
                <button class="btn btn-outline-light btn-sm" @click="unlikeTweet()" v-else-if="likes == true">unlike this tweet</button>
            </div>
            <div class="col"><br>
                <h5># of likes: {{likesCount}}</h5>
            </div>
            <div class="col">
            </div>
            <div class="col">
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
import cookies from 'vue-cookies'

    export default {
        name: "like-tweet",

        data(){
            return {
                tweetLikes: [],
                likes: false,
                likesCount: 0,
                }
        },
        props: {
            tweetId: Number
        },

    mounted(){
        this.getLikes();
    },

    methods: {
        likeTweet(){
            axios.request({
                url: "https://tweeterest.ml/api/tweet-likes",
                method: "POST",
                headers: {
                     'Content-Type': "application/json",
                     "X-Api-Key": "p3JJq3WhdMwT98hN9PTaYDE1lr2p0qKOaLfIdjyDxiorc"
                },
                data: {
                    loginToken: cookies.get('session'),
                    tweetId: this.tweetId,
                }
                }).then((response) => {
                    console.log(response);
                    this.likes = true;
                    this.likesCount++;
                    window.location.reload()
                }).catch((error) => {
                    console.log(error);
                })
        },
        getLikes(){
            axios.request({
                url: "https://tweeterest.ml/api/tweet-likes",
                method: "GET",
                headers: {
                     'Content-Type': "application/json",
                     "X-Api-Key": "p3JJq3WhdMwT98hN9PTaYDE1lr2p0qKOaLfIdjyDxiorc"
                },
                params: {
                    tweetId: this.tweetId,
                }
                }).then((response) => {
                    console.log(response);
                    this.tweetLikes = response.data;
                    this.likesCount = this.tweetLikes.length;
                        let currentUser = cookies.get('userId');
                        for (let i = 0; i < this.tweetLikes.length; i++){
                            if(currentUser == this.tweetLikes[i].userId){
                                this.likes = true;
                            }
                        }

                }).catch((error) => {
                    console.log(error);
                })
        },
        unlikeTweet(){
            axios.request({
                url: "https://tweeterest.ml/api/tweet-likes",
                method: "DELETE",
                headers: {
                    'Content-Type': "application/json",
                    "X-Api-Key": "p3JJq3WhdMwT98hN9PTaYDE1lr2p0qKOaLfIdjyDxiorc"
                },
                data: {
                    loginToken: cookies.get('session'),
                    tweetId: this.tweetId,
                }
                }).then((response) => {
                    console.log(response);
                    this.likes = false;
                    this.likesCount--;
                    window.location.reload()
                }).catch((error) => {
                    console.log(error);
                })
        }
    }
}
</script>

<style scoped>
</style>