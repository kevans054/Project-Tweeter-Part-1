<template>
    <div>
        <div class="row">
            <div class="col">
                <textarea v-model="newBio" placeholder=comment></textarea>
            </div>
        </div>
        <div class="row">
            <div class="col">
                <button class="btn btn-outline-dark btn-sm" type="button" @click="updateProfile()">Update Bio</button>
            </div>
        </div>
    </div>
        
</template>

<script>
import axios from "axios"
import cookies from "vue-cookies"

    export default {
        name: "edit-profile",

        props: {
            userId: {
                type: Number,
                required: true
            },
            bio: {
                type: String,
                required: true
            }
        },
        data() {
            return {
                updatedProfile: [],
                newBio: "",
            }
        },
        
        methods: {
            updateProfile: function() {
                console.log(this.commentId)
                axios.request({
                    url: "https://tweeterest.ml/api/users",
                    method: "PATCH",
                    headers: {
                        "Content-Type": "application/json",
                        "X-Api-Key": "p3JJq3WhdMwT98hN9PTaYDE1lr2p0qKOaLfIdjyDxiorc"
                    }, 
                    data: {
                        loginToken: cookies.get("session"),
                        bio: this.newBio,
                    },
                }).then((response) => {
                    console.log(response)

                }).catch((error) => {
                    console.log(error)
                    console.log(this.newBio)
                })
            }
        },
    }
</script>

<style scoped>

</style>