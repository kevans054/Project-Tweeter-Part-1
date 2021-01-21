<template>
    <div>
        <div class="row">
            <div class="col">
                <textarea v-model="commentContent" placeholder=comment></textarea>
            </div>
        </div>
        <div class="row">
            <div class="col">
                <button class="btn btn-outline-dark btn-sm" type="button" @click="updateComment()">Update Comment</button>
            </div>
        </div>
    </div>
        
</template>

<script>
import axios from "axios"
import cookies from "vue-cookies"

    export default {
        name: "update-comment",

        props: {
            comment: {
                type: String,
                // required: true
            },
            commentId: {
                type: Number,
                // required: true
            }
        },
        data() {
            return {
                updatedComments: [],
                commentContent: "",
            }
        },
        
        methods: {
            updateComment: function() {
                console.log(this.commentId)
                axios.request({
                    url: "https://tweeterest.ml/api/comments",
                    method: "PATCH",
                    headers: {
                        "Content-Type": "application/json",
                        "X-Api-Key": "p3JJq3WhdMwT98hN9PTaYDE1lr2p0qKOaLfIdjyDxiorc"
                    }, 
                    data: {
                        loginToken: cookies.get("session"),
                        commentId: this.commentId,
                        content: this.commentContent

                    },
                }).then((response) => {
                    console.log(response)

                }).catch((error) => {
                    console.log(error)
                    console.log(this.commentId)
                })
            }
        },
    }
</script>

<style scoped>

</style>