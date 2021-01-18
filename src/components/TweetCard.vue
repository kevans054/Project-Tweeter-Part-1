<template>
    <div>
        <h1>This is a tweet</h1>
        <div class="container-fluid">
            <h3>{{ tweetObject.username }}</h3>
            <h6>{{ tweetObject.userId }}</h6>
            
            <p>{{ tweetObject.tweetId}}
            <p>{{ content }}</p>
            <h5>{{ tweetObject.createdAt }}</h5>
            <tweet-delete v-if="isOwned" :tweetId="tweetObject.tweetId"></tweet-delete><br>
            <tweet-edit @update-tweet="updateTweet" v-if="isOwned" :tweetId="tweetObject.tweetId"></tweet-edit><br>
            <view-comments :tweetId="tweetObject.tweetId"></view-comments>
            <add-comments @add-comment="addComment" :tweetid="tweetObject.tweetId"></add-comments>
            <view-profiles :userId="tweetObject.userId"></view-profiles>
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
                // comments: {
                // type: Object,
                // required: true
                // }
            },
        data() {
            return {
                isOwned: cookies.get('userId') == this.tweetObject.userId,
                content: this.tweetObject.content,
            
            }
        },
        methods: {
            updateTweet(newContent) {
                this.content = newContent;
            },

            addComment(newComment) {
                this.comment = newComment;
            },
        //    viewProfile(userId){

        //    }
        },
    }
</script>

<style scoped>
    .container-fluid {
        display: grid;
        border: 10px;
        color: blue;
        margin: 10px;
    }
</style>
