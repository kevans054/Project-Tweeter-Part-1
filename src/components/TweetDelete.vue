<template>
    <div>
        <!-- add alert to confirm delete before -->
        <button class="btn btn-outline-light btn-sm" @click="deleteTweet()">Delete Tweet</button>
    </div>
</template>

<script>
import axios from "axios"
import cookies from "vue-cookies"

    export default {
        name: "tweet-delete",
        
        props: {
            tweetId: {
                type: Number,
                required: true
            }
        },
        methods: {
            deleteTweet: function() {
                axios.request({
                    url: "https://tweeterest.ml/api/tweets",
                    method: "DELETE",
                    headers: {
                        "Content-Type": "application/json",
                        "X-Api-Key": "p3JJq3WhdMwT98hN9PTaYDE1lr2p0qKOaLfIdjyDxiorc"
                    }, 
                    data: {
                        loginToken: cookies.get("session"),
                        tweetId: this.tweetId
                    },
                }).then((response) => {
                    console.log(response)
                    window.location.reload()

                }).catch((error) => {
                    console.log(error)
                })
            }
        },
    }
</script>

<style scoped>

</style>