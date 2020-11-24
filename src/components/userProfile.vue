<template>
  <div class="user-profile">
    <div class="user-profile_user-panel">
      <h1 class="user-profile_username">@{{ user.username }}</h1>
      <div class="user-profile_admin-badge" v-if="user.isAdmin">Admin</div>
      <div class="user-profile_follower-count">
        <strong>Followers</strong> {{ followers }}
      </div>
    </div>
    <div class="user-profile_twoots-wrapper">
      <TwootItem
        v-for="twoot in user.twoots"
        :key="twoot.id"
        :username="user.username"
        :twoot="twoot"
        @favourite="toggleFavourite"
        
      />
    </div>
  </div>
</template>

<script>
import TwootItem from './TwootItem';
export default {
  name: "userProfile",
  components: {TwootItem},
  data() {
    return {
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
          { id: 3, content: "Don't forget to subscribr" },
          { id: 4, content: "Don't forget to subscribr" },
          { id: 5, content: "Don't forget to subscribr" },
        ],
      },
    };
  },
  watch: {
    followers(newFollowAccount, oldFollowAccount) {
      if (oldFollowAccount < newFollowAccount) {
        console.log(`${this.user.username} has gaind followers!`);
      }
    },
  },
  computed: {
    fullName() {
      return `${this.user.firstname} ${this.user.lastname}`;
    },
  },
  methods: {
    followUser() {
      this.followers++;
    },
    toggleFavourite(id){
      console.log(`favourite Tweet #${id}`)
    }
  },
  mounted() {
    this.followUser();
  },
};
</script>

<style>
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  width: 100%;
  padding: 50px 5%;
}
.user-profile_user-panel {
  display: flex;
  flex-direction: column;
  margin-right: 50px;
  padding: 20px;
  background-color: #fff;
  border-radius: 5px;
  border: 1px solid #dfe3e8;
}
.user-profile_admin-badge {
  background: rebeccapurple;
  color: #fff;
  border-radius: 5px;
  margin-right: auto;
  padding: 0 10px;
  font-weight: bold;
}
h1 {
  margin: 0;
}
</style>
