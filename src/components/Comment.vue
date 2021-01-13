<template>
    <div>
        <h3>Comment</h3>
        <div>
            <p>{{ content }}</p>
        </div>
    </div>
</template>

<script>
import cookies from 'vue-cookies'
    export default {
        name: "show-comments",

        props: {
            tweetObject: {
                type: Object,
                required: true 
            },
         data() {
            return {
                isOwned: cookies.get('userId') == this.tweetObject.userId,
                content: this.tweetObject.content,
                // comment: CommentForm.comment
            }
        },
        methods: {
            updateTweet(newContent) {
                this.content = newContent;
            },

            // updateComment(newComment) {
            //     this.comment = newComment;
            // }
        },
    }
    
</script>

<style scoped>

</style>