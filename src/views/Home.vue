<template>
  <div class="home-container">
   
    <div>
      <p>Welcome to Your Tweeter App</p>
    </div>
    <div class="container">
      <login-form v-if="login"></login-form>
      <signup-form v-else></signup-form>
      <p @click="login = !login" v-if="!login">I already have an account</p>
      <p @click="login = !login" v-else>I don't have an account yet</p>
    </div>
    <!-- <router-view/> -->
  </div>
</template>

<script>
// import LoginForm from "../LoginForm.vue";
// import SignupForm from "../SignupForm.vue";

export default {
  name: "Home",

}
</script>
<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

</style>
