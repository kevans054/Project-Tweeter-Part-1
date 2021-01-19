<template>
    <div>
        <div class="container">
            <div class="row row cols-3 alert alert-primary">
                <div class="col ">Username:{{ tweetObject.username }}</div>
                <div class="col">UserId: {{ tweetObject.userId }}</div>
                <div class="col">TweetId: {{ tweetObject.tweetId}}</div>
            </div>
            <div class="row">
                <div class="col-12">
                    <h2>{{ content }}</h2>
                    <p>{{ tweetObject.createdAt }}</p>
                </div>
            </div>
            <div class="row">
                <div class="row row cols-2">
                    <tweet-delete class="col" v-if="isOwned" :tweetId="tweetObject.tweetId"></tweet-delete>
                    <tweet-edit  class="col" @update-tweet="updateTweet" v-if="isOwned" :tweetId="tweetObject.tweetId"></tweet-edit>
                </div>
            </div>
            <div class="row">
                <div class="col-sm-12">
                    <add-comments @add-comment="addComment" :tweetid="tweetObject.tweetId"></add-comments>
                </div>
            </div>
            <div class="row">
                <div class="col-sm-12">
                    <view-comments :tweetId="tweetObject.tweetId"></view-comments>
                </div>
            </div>
            <div class="row">
                <div>
                    <view-profiles :userId="tweetObject.userId"></view-profiles>
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
// import Follow from './Follow.vue'
import cookies from 'vue-cookies'
    export default {
        name: "tweet-card",
        components: {
            TweetDelete,
            TweetEdit,
            AddComments,
            ViewComments,
            ViewProfiles,
            // Follow
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

    .container {
        background-color: rgb(20, 131, 223);
        padding: 30px;
        border-radius: 3%;
        border-end-end-radius: 10%;
        margin: 15px;
    }
    .row {
        /* display:inline-flexbox; */
        border-color: rgb(8, 37, 167);
        border-width: 10px;
        justify-content: center;
    }
</style>
