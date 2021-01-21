<template>
    <div class="container border border-dark rounded">
        <div class="row">
            <div class="col">
                <div class=text-light>
                    <h3>UserName: @{{ tweetObject.username }}</h3>
                </div>
            </div>
        </div>
        <div class="row">
            <div class="col"><br>
                <view-profiles :userId="tweetObject.userId"></view-profiles>
                <br>
            </div>
        </div>
        <div class="container border">
            <div class="row">
                <div class="col"><br>
                    <h6>{{ tweetObject.createdAt }}</h6>
                </div>
            </div>
            <div class="row">
                <div class="col">
                        <h5>"{{ content }}"</h5>
                </div>
            </div>
            <div class="row">
                    <div class="col">
                        <like-tweet :tweetId="tweetObject.tweetId"></like-tweet>
                        <br>
                    </div>
                </div>
            <div class="row">
                <div class="col">
                </div>
                <div class="col">
                </div>
                <div class="col">
                    <tweet-delete class="col" v-if="isOwned" :tweetId="tweetObject.tweetId"></tweet-delete>
                </div>
                <div class="col">
                    <tweet-edit class="col" @update-tweet="updateTweet" v-if="isOwned" :tweetId="tweetObject.tweetId"></tweet-edit>
                    <br>
                </div>
                <div class="col">
                </div>
                <div class="col">
                </div>
            </div>
        </div>
        <div class="container border">
            <div class="row">
                <div class="col"><br>
                    <add-comments @add-comment="addComment" :tweetid="tweetObject.tweetId"></add-comments>
                </div>
                <div class="row">
                    <div class="col">
                    </div>
                    <div class="col">
                        <button class="btn btn-outline-light btn-sm" @click="show = !show">View All Comments</button>
                            <div v-if="show">
                                <view-comments :tweetId="tweetObject.tweetId"></view-comments>
                            </div>
                    </div>
                    <div class="col"><br><br>
                </div>
                </div>
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
                content: this.tweetObject.content,
                show: false
            }
        },
        methods: {
            reloadPage() {
                window.location.reload()
            },
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
