<template>
    <div id="profile">
        <div>
            <h1>User Profile</h1>
        </div>
        <div>
            <div v-for="user in users" :key="user.userId">
                <p>Email: {{ user.email }}</p>
                <p>Username: {{ user.username }}</p>
                <p>Bio: {{user.bio }}</p>
                <p>birthdate: {{ user.birthdate }}</p>
                <p> userId: {{user.userId}}</p><br>
                <button @click="show = !show">Edit Profile</button>
                    <div v-if="show">
                        <p>Bio: </p> <textarea v-model="bioUpdate"></textarea><br><br>
                        <button @click="saveUser()">Submit</button>
                    </div>
            </div>
        </div>
        
    </div>
</template>

<script>
import axios from 'axios'
import cookies from 'vue-cookies'

    export default {
        name: "user-profile",


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
                        
                        // email: this.email,
                        // username: "",
                        // password: "",
                        // bio: "",
                        // birthdate: "",
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
            },
            // edit: function(){
            //     isOwned: cookies.get('userId') == this.userId

            // },
            deleteUser: function() {
                    
                    axios.request({
                    url: "https://tweeterest.ml/api/users",
                    method: "DELETE",
                    headers: {
                        "Content-Type": "application/json",
                        "X-Api-Key": "p3JJq3WhdMwT98hN9PTaYDE1lr2p0qKOaLfIdjyDxiorc"
                    },
                    data: {
                        loginToken: cookies.get("session"),
                        password: cookies.get("Userpassword")
                        
                    },
                    }).then((response) => {
                        console.log(response)
                       
                    }).catch((error) => {
                        console.log(error)
                    })
                },
        }
    }
</script>

<style scoped>

</style>