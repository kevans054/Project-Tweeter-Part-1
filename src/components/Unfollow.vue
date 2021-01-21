<template>
    <div>
        <button @click="unfollow" v-if="unfollow == true">unfollow this user</button>
    </div>
</template>

<script>
import axios from "axios"
import cookies from "vue-cookies"
    export default {
        name: 'unfollow-user',
    

    unfollow(){
            axios.request({
                url: "https://tweeterest.ml/api/follows",
                method: "DELETE",
                headers: {
                     'Content-Type': "application/json",
                     "X-Api-Key": "p3JJq3WhdMwT98hN9PTaYDE1lr2p0qKOaLfIdjyDxiorc"
                },
                data: {
                    loginToken: cookies.get('session'),
                    followId: this.userId,
                }
                }).then((response) => {
                console.log(response);
                this.following = false;
                this.followerCount--;
                }).catch((error) => {
                console.log(error);
                })
        },
}
</script>

<style scoped>

</style>

