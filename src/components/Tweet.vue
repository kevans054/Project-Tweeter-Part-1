<template>
    <div class="tweet-container">
        <h3>This is a tweet</h3>
        <div>
            <h3>{{ tweetObject.username }}</h3>
            <h6>{{ tweetObject.userId }}</h6>
            <p>{{ content }}</p>
            <h5>{{ tweetObject.createdAt }}</h5>
            <tweet-delete v-if="isOwned" :tweetId="tweetObject.tweetId"></tweet-delete><br>
            <tweet-edit @update-tweet="updateTweet" v-if="isOwned" :tweetId="tweetObject.tweetId"></tweet-edit>
        </div>
    </div>
</template>

<script>
import TweetDelete from './TweetDelete.vue'
import TweetEdit from './TweetEdit.vue'
import cookies from 'vue-cookies'
    export default {
        name: "page-tweet",
        components: {
            TweetDelete,
            TweetEdit
        },
        props: {
            tweetObject: {
                type: Object,
                required: true 
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
            }
        },
    }
</script>

<style scoped>
    .tweet-container {
        display: grid;
        margin: 10px;
    }
</style>
