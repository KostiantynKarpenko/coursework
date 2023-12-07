<template>
  <div class="login-window">
    <h3 class="title">Sign up</h3>
    <div class="form">
      <div class="email-input cred-input">
        <input type="text" placeholder="Email" v-model="userCred.email">
      </div>
      <div class="password-input cred-input">
        <input type="password" placeholder="Password" v-model="userCred.firstPassword">
      </div>
      <div class="password-input cred-input">
        <input type="password" placeholder="Confirm password" v-model="userCred.secondPassword">
      </div>      
    </div>
    <div class="login-actions">
      <button @click="signIn()" class="btn">Sign in</button>
      <button @click="signUp()" class="btn">Sign up</button>
    </div>
  </div>
</template>

<script>
import router from '@/router';

export default {
  name: 'SignupWindow',
  data(){
    return {
      userCred:{
        email: '',
        firstPassword: '',
        secondPassword: '',
      }
    }
  },
  methods:{
    signIn(){
      router.push('/')
    },
    signUp(){
      if (this.userCred.firstPassword.length >= 6 || this.userCred.secondPassword.length >= 6){
        if (this.userCred.firstPassword == this.userCred.secondPassword){
          this.$store.dispatch('signUp', this.userCred)
        }
        else{
          console.log('Passwords doesn\'t match');
        }
      }
      else{
        console.log('Password should contain at least 6 characters');
      }
    },
  }
}
</script>

<style scoped lang="less">

</style>
