<template>
    <div class="tweet-container">
        <h3>This is a tweet</h3>
        <div>
            <h3>{{ tweetObject.username }}</h3>
            <p>{{ tweetObject.content }}</p>
            <h5>{{ tweetObject.createdAt }}</h5>
        </div>
    </div>
</template>

<script>
    export default {
        name: "page-tweet",
        props: {
            tweetObject: {
                type: Object,
                required: true 
            },
        },
    }
</script>

<style scoped>
    .tweet-container {
        display: grid;
        margin: 10px;
    }
</style>
