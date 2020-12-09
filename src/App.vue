<template>
  <div id="app">
    <nav>
      <div class="nav_logo">Twooter</div>

      <div class="nav_user">
        {{ user.username }}
      </div>
    </nav>

    <userProfile />
  </div>
</template>

<script>
import userProfile from "./components/userProfile";

export default {
  name: "app",
  components: { userProfile },
  data() {
    return {
      user: {
        username: "_Mostafa-Muatz",
      },
    };
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  min-height: 100vh;
  background-color: #f3f5fa;

  nav {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 10px 5%;
    background-color: deeppink;
    color: #fff;

    .nav_logo {
      font-size: 24px;
      font-weight: bold;
    }

    .nav_user {
      font-weight: bold;
    }
  }
}
</style>
