<template>
    <div class="container border" id="profile">
        <button class="btn btn-outline-light btn-sm" @click="show = !show">View User Profile</button>
        <div v-if="show">
            <h1>User Profile</h1>
            <div class="row">
                <div class="col" v-for="user in users" :key="user.userId">
                    <p>Email: {{ user.email }}</p>
                    <p>Username: {{ user.username }}</p>
                    <p>Bio: {{user.bio }}</p>
                    <p>birthdate: {{ user.birthdate }}</p>
                    <p> userId: {{user.userId}}</p><br>
                    <follow-user :userId="user.userId"></follow-user>
                    <div v-if="userId == user.userId">
                        <edit-profile :userId="user.userId" :bio="user.bio"></edit-profile><br>
                        <delete-profile></delete-profile><br>
                    </div>
                </div>
            </div>
        </div>        
        
    </div>
</template>

<script>
import axios from 'axios'
// import cookies from 'vue-cookies'
import DeleteProfile from './DeleteProfile.vue'
import EditProfile from "./EditProfile.vue"
import FollowUser from "./Follow.vue"

    export default {
        name: "view-profiles",

    components: {
        DeleteProfile,
        EditProfile,
        FollowUser
    },

         data() {
            return {
                users: [],
                loginToken: "",
                bioUpdate: "",
                password: "",
                show: false
                }
            },
            props: {
                userId: {
                type: Number,
                required: true 
                }
            },
            mounted: function() {
            this.getUser();
        },
            methods: {
                getUser: function() {
                    axios.request({
                    url: "https://tweeterest.ml/api/users",
                    method: "GET",
                    headers: {
                        "Content-Type": "application/json",
                        "X-Api-Key": "p3JJq3WhdMwT98hN9PTaYDE1lr2p0qKOaLfIdjyDxiorc"
                    },
                    params: {
                        userId: this.userId
                        
                    },
                    }).then((response) => {
                        console.log(response)
                        this.users = response.data

                    }).catch((error) => {
                        console.log(error)
                    })
                },
                
            
        }
    }
</script>

<style scoped>

</style>