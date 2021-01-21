<template>
    <div>
        <div>
            <button class="btn btn-outline-dark btn-sm" @click="deleteComment()">Delete Comment</button>
        </div>
    </div>
        
</template>

<script>
import axios from "axios"
import cookies from "vue-cookies"

    export default {
        name: "delete-comment",
        
        methods: {
            deleteComment: function() {
                axios.request({
                    url: "https://tweeterest.ml/api/comments",
                    method: "DELETE",
                    headers: {
                        "Content-Type": "application/json",
                        "X-Api-Key": "p3JJq3WhdMwT98hN9PTaYDE1lr2p0qKOaLfIdjyDxiorc"
                    }, 
                    data: {
                        loginToken: cookies.get("session"),
                        commentId: cookies.get("commentId")
                    },
                }).then((response) => {
                    console.log(response)
                    window.location.reload()
                }).catch((error) => {
                    console.log(error)
                })
            }
        },
    }
</script>

<style scoped>

</style>