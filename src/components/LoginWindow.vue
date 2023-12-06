<template>
  <div class="login-window">
    <h3 class="title">Login</h3>
    <div class="form">
      <div class="email-input cred-input">
        <input type="text" placeholder="Email" v-model="userCred.email">
      </div>
      <div class="password-input cred-input">
        <input type="password" placeholder="Password" v-model="userCred.password">
        <img src="../assets/img/svg/Eye.svg" alt="">
      </div>
    </div>
    <div class="login-actions">
      <button @click="signUp()" class="btn">Sign up</button>
      <button @click="signIn()" class="btn">Sign in</button>
    </div>
  </div>
</template>

<script>
import router from '@/router';

export default {
  data(){
    return {
      userCred:{
        email: '',
        password: '',
      }
    }
  },
  name: 'LoginWindow',
  components: {
  },
  props: {
  },
  methods:{
    signIn(){
      this.$store.dispatch('signIn', this.userCred)
    },
    signUp(){
      router.push('/signup')
    },
  },
}
</script>

<style scoped lang="less">

</style>
