<template>
    <div id="feed-title">
        <p>My Tweeter Feed</p>
        <tweet-form></tweet-form>
    </div>
</template>

<script>
import TweetForm from "../components/TweetForm.vue"
    export default {
        name: "feed-page",
        components: {
            TweetForm,
        },
    }
</script>

<style lang="sass" scoped>

</style>