<template>
<div class="container">
    
    <div class="row">
        <div class="col">
            <h4>Delete your account</h4><br>
            <p>Password required:
        <input type="password" id="password" v-model="password" class="starndard-input"></p>
        <button @click="deleteAccount" class="button is-info">Confirm Delete</button>
        </div>
    </div>
    <div>
        
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
                        password: this.userpassword,
                    }
                }).then((response) => {
                    console.log(response)
                    cookies.sdelete('session');
                    cookies.delete('userId');
                    this.$router.push("/SignupForm")

                }).catch((error) => {
                    console.log(error)
                })
            }
        },
  
            

    }
</script>

<style scoped>

</style>