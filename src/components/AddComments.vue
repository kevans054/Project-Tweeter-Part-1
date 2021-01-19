<template>
    <div>
        <div class="row row cols-12">
            <div class="col-12">
                <h3>Add Comments</h3>
            </div>
        </div>
        <div class="row">
            <textarea class="text-primary col-12" v-model="tweetComment"></textarea>
        </div><br>
        <button type="submit" class="btn btn-sm btn-primary btn-block Mybutton" @click="postComment()">Submit</button>
        
    </div>
</template>

<script>
import cookies from 'vue-cookies'
import axios from "axios"
    export default {
        name: "add-comments",

        data() {
             
            return {
                comments: [],
                tweetComment: "",
            }
        },
        props: {
            tweetid: {
                type: Number,
                required: true 
            },
        },
        methods: {
            postComment: function() {
                
                axios.request({
                    url: "https://tweeterest.ml/api/comments",
                    method: "POST",
                    headers: {
                        "Content-Type": "application/json",
                        "X-Api-Key": "p3JJq3WhdMwT98hN9PTaYDE1lr2p0qKOaLfIdjyDxiorc"
                    }, 
                    data: {
                        loginToken: cookies.get("session"),
                        tweetId: this.tweetid,
                        content: this.tweetComment
                        
                    },
                     
                }).then((response) => {
                    console.log(response)
                    // this.$emit('update-comment', this.tweetComment)
                    // this.show = false;

                }).catch((error) => {
                    console.log(error)
                })
            }
        }
    }
    
</script>

<style scoped>
  .Mybutton{
        align-items: center;
        background-color: rgb(11, 111, 241);
        border-color: darkmagenta;
        border-width: thick;
    }
</style>