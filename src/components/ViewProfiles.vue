<template>
    <div id="profile">
        <button @click="show = !show">View User Profile</button>
        <div v-if="show">
            <h1>User Profile</h1>
        
        
        <div>
            <div v-for="user in users" :key="user.userId">
                <p>Email: {{ user.email }}</p>
                <p>Username: {{ user.username }}</p>
                <p>Bio: {{user.bio }}</p>
                <p>birthdate: {{ user.birthdate }}</p>
                <p> userId: {{user.userId}}</p><br>
                
            </div>
            </div>
        </div>        
        
    </div>
</template>

<script>
import axios from 'axios'
// import cookies from 'vue-cookies'

    export default {
        name: "view-profiles",


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
                        
                        // email: this.email,
                        // username: "",
                        // password: "",
                        // bio: "",
                        // birthdate: "",
                    }).catch((error) => {
                        console.log(error)
                    })
                },
                
            
        }
    }
</script>

<style scoped>

</style>