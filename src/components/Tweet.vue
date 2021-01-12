<template>
    <div class="tweet-container">
        <h3>This is a tweet</h3>
        <div>
            <h3>{{ tweetObject.username }}</h3>
            <h6>{{ tweetObject.userId }}</h6>
            <p>{{ tweetObject.content }}</p>
            <h5>{{ tweetObject.createdAt }}</h5>
            <tweet-delete v-if="isOwned" :tweetId="tweetObject.tweetId"></tweet-delete>
        </div>
    </div>
</template>

<script>
import TweetDelete from'./TweetDelete.vue'
import cookies from 'vue-cookies'
    export default {
        name: "page-tweet",
        components: {
            TweetDelete
        },
        props: {
            tweetObject: {
                type: Object,
                required: true 
            },
        },
        data() {
            return {
                isOwned: cookies.get('userId') == this.tweetObject.userId
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
