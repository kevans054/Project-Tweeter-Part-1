<template>
    <div class="container border">
        <div class="row">
            <div class="col">
                <h1>User Profile</h1>
            </div>
        </div>
        <div class="row">
            <div class="col">
                <div v-for="user in users" :key="user.userId">
                    <p>Email: {{ user.email }}</p>
                    <p>Username: {{ user.username }}</p>
                    <p>Bio: {{user.bio }}</p>
                    <p>birthdate: {{ user.birthdate }}</p>
                    <p> userId: {{user.userId}}</p><br>
                    <button class="btn btn-outline-dark btn-sm" @click="show = !show">Edit Profile</button><br><br>
                        <div v-if="show">
                            <p>Bio: </p> <textarea v-model="bioUpdate"></textarea><br><br>
                            <button class="btn btn-outline-dark btn-sm" @click="saveUser()" placeholder="user.bio">Save Changes</button><br><br>
                        </div>
                </div>
            </div>
        </div>
        <div class="row">
            <div class="col">
                <delete-profile></delete-profile>
            </div>
        </div>
    </div>
</template>

<script>
import axios from 'axios'
import cookies from 'vue-cookies'
import DeleteProfile from './DeleteProfile.vue'

    export default {
        name: "user-profile",
        components: {
            DeleteProfile
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
                        userId: cookies.get("userId")
                    }
                    }).then((response) => {
                        console.log(response)
                        this.users = response.data

                    }).catch((error) => {
                        console.log(error)
                    })
                },
                saveUser: function() {
                    axios.request({
                        method: "PATCH",
                        url: "https://tweeterest.ml/api/users",
                        headers: {
                            "Content-Type": "application/json",
                            "X-Api-Key": "p3JJq3WhdMwT98hN9PTaYDE1lr2p0qKOaLfIdjyDxiorc"
                        },
                        data: {
                            loginToken: cookies.get('session'),
                            bio: this.bioUpdate,
                        }
                    }).then((response) => {
                        console.log(response)
                        
                    }).catch((error) => {
                        console.log(error)
                    })
            }
        }
    }
</script>

<style scoped>
    .container {
        background-color: rgb(20, 131, 223);
    }
</style>