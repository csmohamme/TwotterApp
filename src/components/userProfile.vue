<template>
  <div class="user-profile">
    <div class="user-profile_sidebar">
      <div class="user-profile_user-panel">
        <h1 class="user-profile_username">@{{ state.user.username }}</h1>
        <div class="user-profile_admin-badge" v-if="state.user.isAdmin">
          Admin
        </div>
        <div class="user-profile_follower-count">
          <strong>Followers</strong> {{ state.followers }}
        </div>
      </div>
      <CreateTwootPanel @add-twoot="addTwoot" />
    </div>
    <div class="user-profile_twoots-wrapper">
      <TwootItem
        v-for="twoot in state.user.twoots"
        :key="twoot.id"
        :username="state.user.username"
        :twoot="twoot"
      />
    </div>
  </div>
</template>

<script>
import { reactive } from "vue";

import TwootItem from "./TwootItem";

import CreateTwootPanel from "./CreateTwootPanel";

export default {
  name: "userProfile",
  components: { CreateTwootPanel, TwootItem },

  setup() {
    const state = reactive({
      followers: 0,
      user: {
        id: 1,
        username: "_Wad_Muatz",
        firstname: "mostafa",
        lastname: "muatz",
        email: "mostafa@gmail.com",
        isAdmin: true,
        twoots: [
          { id: 1, content: "this is nice" },
          { id: 2, content: "Don't forget to subscribr" },
        ],
      },
    });
    function addTwoot(twoot) {
      state.user.twoots.unshift({
        id: state.user.twoots.length + 1,
        content: twoot,
      });
    }
    return {
      state,
      addTwoot,
    };
  },
};
</script>

<style lang="scss" scoped>
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  grid-gap: 50px;
  padding: 50px 5%;

  .user-profile_user-panel {
    display: flex;
    flex-direction: column;
    padding: 20px;
    background-color: #fff;
    border-radius: 5px;
    border: 1px solid #dfe3e8;
    margin-bottom: auto;

    h1 {
      margin: 0;
    }

    .user-profile_admin-badge {
      background: rebeccapurple;
      color: #fff;
      border-radius: 5px;
      margin-right: auto;
      padding: 0 10px;
      font-weight: bold;
    }
  }
  .user-profile_twoots-wrapper {
    display: grid;
    grid-gap: 10px;
    margin-bottom: auto;
  }
}
</style>
