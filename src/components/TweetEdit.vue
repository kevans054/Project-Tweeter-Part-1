<template>
    <div>
        <button class="btn btn-outline-light btn-sm" type="button" @click="show = !show">Edit Tweet</button>
        <div v-if="show">
            <textarea v-model="tweetContent"></textarea>
            <button class="btn btn-outline-light" type="button" @click="editTweet()">Submit</button>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
import cookies from 'vue-cookies'
    export default {
        name: 'tweet-edit',
        data() {
            return {
                show: false,
                tweetContent: ""
            }
        },
        props: {
            tweetId: {
                type: Number,
                required: true 
            },
        },
        methods: {
            editTweet: function() {
                axios.request({
                    url: "https://tweeterest.ml/api/tweets",
                    method: "PATCH",
                    headers: {
                        "Content-Type": "application/json",
                        "X-Api-Key": "p3JJq3WhdMwT98hN9PTaYDE1lr2p0qKOaLfIdjyDxiorc"
                    }, 
                    data: {
                        loginToken: cookies.get("session"),
                        tweetId: this.tweetId,
                        content: this.tweetContent
                    },
                     
                }).then((response) => {
                    console.log(response)
                    this.$emit('update-tweet', this.tweetContent)
                    this.show = false;

                }).catch((error) => {
                    console.log(error)
                })
            }
        },
    }
</script>

<style scoped>

</style>