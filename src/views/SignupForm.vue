<template class="container border">
    <div>
        <div class="row">
            <div class="col">
                <h4 class="text-info">Create your account</h4>
            </div>
        </div>
        <div class="row">
            <div class="col">
                <p>Email:
                <input type="text" id="emailfield" v-model="email" class="starndard-input" placeholder="Email address"></p>
            </div>
        </div>
        <div class="row">
            <div class="col">
                <p>Username:
                <input type="text" id="usernamefield" v-model="username"></p>
            </div>
        </div>
        <div class="row">
            <div class="col">
                <p>Password:
                <input type="password" id="passwordfield" v-model="userpassword" placeholder="password"> </p>
            </div>
        </div>
        <div class="row">
            <div class="col">
                <p>Bio:
                <input type="text" id="biofield" v-model="bio"></p>
            </div>
        </div>
        <div class="row">
            <div class="col">
                <p>birthdate:
                <input type="text" id="birthdatefield" v-model="birthdate" placeholder="yyyy-mm-dd"></p>
            </div>
        </div>
        <div class="row">
            <div class="col">
                <button class="btn btn-outline-dark btn-sm" @click="signupUser">Sign up</button>
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
/* .container {
        background-color: rgb(20, 131, 223);
    } */
</style>