<template>
    <div>
        <div class="row">
            <div class="col">
                <h1 class="text-info">Create your account</h1>
            </div>
        </div>
        <div class="container border">
                <div class="row">
                    <div class="col"><br><br>
                        <input type="text" label="1" id="emailfield" v-model="email" class="starndard-input" placeholder="Email address">
                    </div>
                </div>
                <div class="row">
                    <div class="col"><br>
                        <input type="text" id="usernamefield" v-model="username" class="standard-input" placeholder="Username">
                    </div>
                </div>
                <div class="row">
                    <div class="col"><br>
                        <input type="password" id="passwordfield" v-model="userpassword" placeholder="Password">
                    </div>
                </div>
                <div class="row">
                    <div class="col"><br>
                        <input type="text" id="biofield" v-model="bio" class="standard-input" placeholder="Bio">
                    </div>
                </div>
                <div class="row">
                    <div class="col"><br>
                        <input type="text" id="birthdatefield" v-model="birthdate" class="standard-input" placeholder="Birthdate: yyyy-mm-dd">
                    </div>
                </div>
                <div class="row">
                    <div class="col"><br>
                        <button class="btn btn-outline-dark btn-sm" @click="signupUser">Sign up</button>
                        <br><br>
                    </div>
                </div>
 
        </div>
    </div>
</template>

<script>
    import axios from 'axios'
    import cookies from 'vue-cookies'

    export default {
        name: 'SignupForm',

        data() {
            return {
                userId: Number,
                email: "",
                username: "",
                password: "",
                bio: "",
                birthdate: "",
                loginToken: "",
                userpassword: ""
            }
        },
        methods: {
            signupUser: function() {
                
                axios.request({
                    method: "POST",
                    url: "https://tweeterest.ml/api/users",
                    headers: {
                        "Content-Type": "application/json",
                        "X-Api-Key": "p3JJq3WhdMwT98hN9PTaYDE1lr2p0qKOaLfIdjyDxiorc"
                    },
                    data: {
                        email: this.email,
                        username: this.username,
                        password: this.userpassword,
                        bio: this.bio,
                        birthdate: this.birthdate
                    }
                }).then((response) => {
                    console.log(response)
                    cookies.set('session', response.data.loginToken)
                    cookies.set('userId', response.data.userId)
                    cookies.set('userName', response.data.userName)
                    cookies.set('Userpassword', "userpassword"),
                    this.$router.push("/feed")
                }).catch((error) => {
                    console.log(error)
                })
            }
        },
  
    }
</script>

<style scoped>
.container {
        background-color: rgb(20, 131, 223);
    }
</style>