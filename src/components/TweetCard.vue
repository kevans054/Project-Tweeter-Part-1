<template>
    <div class="container border border-dark rounded">
        <div>       
            <div class="row">
                <div class="col">
                    <div >@{{ tweetObject.username }}
                    </div>
                </div>
            </div>
            <div class="row">
                <div class="col"><br>
                    <view-profiles :userId="tweetObject.userId"></view-profiles>
                </div>
            </div>
        </div>
        <div id="tweet-info">
            <div class="row">
                <div class="col">
                    <p>{{ tweetObject.createdAt }}</p>
                </div>
                <div class="row">
                    <div class="col">
                        <h5>"{{ content }}"</h5>
                    </div>
                </div>
                <like-tweet :tweetId="tweetObject.tweetId"></like-tweet> 
                <div class="row">
                    <div class="col">
                        <tweet-delete class="col" v-if="isOwned" :tweetId="tweetObject.tweetId"></tweet-delete>
                    </div>
                    <div class="col">
                        <tweet-edit  class="col" @update-tweet="updateTweet" v-if="isOwned" :tweetId="tweetObject.tweetId"></tweet-edit>
                    </div>
                </div>
            </div>
            <div class="row">
                <div class="col"><br>
                    <view-comments :tweetId="tweetObject.tweetId"></view-comments>
                </div>
            </div>
            <div class="row">
                <div class="col"><br>
                    <add-comments @add-comment="addComment" :tweetid="tweetObject.tweetId"></add-comments>
                </div>
            </div>
            <div class="row">
                <div class="col"><br>
                    <div>
                        <button class="btn btn-outline-light btn-sm" @click="reloadPage()">Refresh Tweets</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import TweetDelete from './TweetDelete.vue'
import TweetEdit from './TweetEdit.vue'
import AddComments from './AddComments.vue'
import ViewComments from './ViewComments.vue'
import ViewProfiles from './ViewProfiles.vue'
import LikeTweet from './Like.vue'
import cookies from 'vue-cookies'
    export default {
        name: "tweet-card",
        components: {
            TweetDelete,
            TweetEdit,
            AddComments,
            ViewComments,
            ViewProfiles,
            LikeTweet
        },
        props: {
            tweetObject: {
                type: Object,
                required: true,
                },
            },
        data() {
            return {
                isOwned: cookies.get('userId') == this.tweetObject.userId,
                content: this.tweetObject.content
            }
        },
        methods: {
            updateTweet(newContent) {
                this.content = newContent;
            },

            addComment(newComment) {
                this.comment = newComment;
            },
        },
    }
</script>

<style scoped>

     p {
         font-size: 12px;
    }
    .container {
        background-color: rgb(20, 131, 223);
    }
</style>
