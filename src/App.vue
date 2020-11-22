<template>
  <div id="app">
    @{{ user.username }} -{{ fullName }}
    <strong>Followers</strong> {{ followers }}
    <button @click="followUser">follw</button>
  </div>
</template>

<script>

  export default {
    name: 'App',
    data() {
      return{
      followers:0,
      user:{
        id: 1,
        username: '_Wad_Muatz',
        firstname: 'mostafa',
        lastname: 'muatz',
        email: 'mostafa@gmail.com',
        isAdmin: true
      }
    
      }
      
    },
    computed:{
        fullName() {
          return `${this.user.firstname} ${this.user.lastname}`;
        }
      },
      methods:{
        followUser(){
          this.followers++
        }
      },
      mounted(){
        this.followUser();
      }
    
  }
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  display: flex;
  flex-direction: column;
}
</style>
