<template>
    <div class="container">
        <div class="row">
            <div class="col">
                <h4>Delete your account</h4><br>
                <p>Password required:
                <input type="password" id="password" v-model="password" class="starndard-input"></p>
                <button class="btn btn-outline-dark btn-sm" @click="deleteAccount">Confirm Delete</button>
            </div>
        </div>
    </div>
</template>

<script>
    import axios from 'axios'
    import cookies from 'vue-cookies'

    export default {
        name: 'delete-profile',
        data () {
            return {
            password: ""
            }
        },
        methods: {
            deleteAccount: function() {
                axios.request({
                    url: "https://tweeterest.ml/api/users",
                    method: "DELETE",
                    headers: {
                        "Content-Type": "application/json",
                        "X-Api-Key": "p3JJq3WhdMwT98hN9PTaYDE1lr2p0qKOaLfIdjyDxiorc"
                    },
                    data: {
                        loginToken: cookies.get('session'),
                        password: this.password,
                    }
                }).then((response) => {
                    console.log(response)
                    cookies.delete('session')
                    cookies.delete('userId')
                    this.$router.push("../views/SignupForm")
                    

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