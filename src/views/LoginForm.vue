<template>
    <div id="login">
        <div id="title">
             <div id="login-logo">
                <img src="../assets/twitterlogo.png" alt="Twitter logo">
            </div>
            <p>Welcome to Your Tweeter App</p>
        </div>
        <div class="container">

      <form class="form-signin">
        <h2 class="form-signin-heading">Please sign in</h2>
        <!-- <label for="inputEmail" class="sr-only">Email address</label> -->
        <input type="email" id="inputEmail" class="form-control" v-model="email" placeholder="Email address" required="" autofocus=""><br>
        <!-- <label for="inputPassword" class="sr-only">Password</label> -->
        <input type="password" id="inputPassword" class="form-control" v-model="password" placeholder="Password" required="">
        
        <div>
            <button @click="loginUser" class="btn btn-lg btn-primary btn-block" type="submit">Sign in</button>
        </div><br>
        <div>
            <button @click="signup" class="btn btn-lg btn-primary btn-block">I don't have an account yet</button>
        </div>
      </form>

    </div>
        <!-- <div>
            <h1>Email: </h1><input type="text" id="email-input" v-model="email">
        </div>
        <div>
            <h1>Password: </h1><input type="password" id="password-input" v-model="password">
        </div>
        <div>
            <button @click="loginUser">Login</button>
            <h3 id="login-status">{{loginStatus}}</h3>
            <button @click="signup">I don't have an account yet</button>
             
        </div> -->
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
                })
            },

            signup: function(){
            this.$router.push({ name: 'SignupForm' })
            }
        }
    }
    
</script>

<style lang="sass" scoped>

</style>

