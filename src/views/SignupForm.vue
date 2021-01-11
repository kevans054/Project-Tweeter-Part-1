<template>
<div class="signup">
    <div id="login-logo">
        <img src="../assets/twitterlogo.png" alt="Twitter logo">
    </div>
    <div class="signupData">
        <h4>Create your account</h4>
        <p>Email:
        <input type="text" id="emailfield" v-model="email" class="starndard-input"></p>
        <p>Username:
        <input type="text" id="usernamefield" v-model="username"></p>
        <p>Password:
        <input type="password" id="passwordfield" v-model="password" > </p>
        <p>Bio:
        <input type="text" id="biofield" v-model="bio"></p>
        <p>birthdate:
        <input type="text" id="birthdatefield" v-model="birthdate" placeholder="yyyy-mm-dd"></p>
    </div>
    <div>
        <button @click="signupUser" class="button is-info">Sign up</button>
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
                loginToken: ""
                
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
                        password: this.password,
                        bio: this.bio,
                        birthdate: this.birthdate
                    }
                }).then((response) => {
                    console.log(response)
                    cookies.set('session', response.data.loginToken)
                    cookies.set('userId', response.data.userId)
                    cookies.set('userName', response.data.userName)
                    this.$router.push("/feed")
                }).catch((error) => {
                    console.log(error)
                })
            }
        },
  
            

    }
</script>

<style lang="sass" scoped>

</style>