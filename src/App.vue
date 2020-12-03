<template>
  <div id="app">
    <userProfile/>
  </div>
</template>

<script>
import userProfile from './components/userProfile';
export default {
  name: "app",
  components : {userProfile},
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  // display: flex;
  // flex-direction: column;
  min-height: 100vh;
  background-color: #F3F5FA;
}
</style>
