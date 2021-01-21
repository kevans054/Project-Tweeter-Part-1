<template>
    <div id="login">
        <div id="title"><br>
            <h1 class="text-info">Welcome to Tweeter!</h1>
            <br>
        </div>
        <div class="container border border-dark rounded"><br>
            <form class="form-signin" @submit.prevent="loginUser">
            <h2 class="form-signin-heading">Please sign in</h2><br>
            <input type="email" id="inputEmail" class="form-control" v-model="email" placeholder="Email address"><br>
            <input type="password" id="inputPassword" class="form-control" v-model="password" placeholder="Password">
            <div><br>
                <button  class="btn btn-outline-light btn-sm" type="submit">Sign in</button>
                <br><br>
            </div>
            <div>
                <button class="btn btn-outline-light btn-sm" @click="signup">I don't have a User account</button>
                <br><br>
            </div>
            </form>
        </div>
    </div>
</template>

<script>
    import axios from 'axios'
    import cookies from 'vue-cookies'

    export default {
        name: "LoginForm",
    
        data() {
            return {
                email: "",
                password: "",
                loginStatus: "",
            }
        },
        methods: {
            loginUser: function() {
                this.loginStatus = "Loading",
                
                axios.request({
                    method: "POST",
                    url: "https://tweeterest.ml/api/login",
                    headers: {
                        "Content-Type": "application/json",
                        "X-Api-Key": "p3JJq3WhdMwT98hN9PTaYDE1lr2p0qKOaLfIdjyDxiorc"
                    },
                    data: {
                        email: this.email,
                        password: this.password,
                        loginStatus: this.loginStatus
                    }
                }).then((response) => {
                    this.loginStatus = "Success"
                    cookies.set('session', response.data.loginToken)
                    cookies.set('userId', response.data.userId)
                    cookies.set('Userpassword', "password"),
                    this.$router.push("/feed")
                }).catch((error) => {
                    console.log(error)
                    this.loginStatus = "Error"
                    alert("No account with that email or password found. Please create your account.")
                    this.$router.push({ name: 'SignupForm' })
                })
            },

            signup: function(){
            this.$router.push({ name: 'SignupForm' })
            }
        }
    }
    
</script>

<style scoped>
    .container {
        background-color: rgb(20, 131, 223);
    }
</style>

