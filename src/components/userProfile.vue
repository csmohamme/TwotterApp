<template>
  <div class="user-profile">
    <div class="user-profile_user-panel">
      <h1 class="user-profile_username">@{{ user.username }}</h1>
      <div class="user-profile_admin-badge" v-if="user.isAdmin">Admin</div>
      <div class="user-profile_follower-count">
        <strong>Followers</strong> {{ followers }}
      </div>

      <form class="user-profile_createTwoot" @submit.prevent="createNewTwoot">
        <label for="newTwoot"><strong>New Twoot</strong></label>
        <textarea id="newtwoot" rows="4" v-model="newTwootContent"></textarea>

        <div class="user-profile_createTwoot-type">
          <label for="createTwootType">Type: </label>
          <select id="createTwootType" v-model="selectTwootType">
            <option
              :value="option.value"
              v-for="(option, index ) in twootType"
              :key="index"
            >
              {{ option.name }}
            </option>
          </select>
        </div>
        <button>
          Twoot!
        </button>
      </form>
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
import TwootItem from "./TwootItem";
export default {
  name: "userProfile",
  components: { TwootItem },
  data() {
    return {
      newTwootContent:'',
      selectTwootType:'instant',
      twootType: [
        { value: "draft", name: "Draft" },
        { value: "instant", name: "Instant twoot" },
      ],
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
    toggleFavourite(id) {
      console.log(`favourite Tweet #${id}`);
    },
    createNewTwoot(){
      if(this.newTwootContent && this.selectTwootType !== 'draft'){
        this.user.twoots.unshift({
          id:this.user.twoots.length+1,
          content:this.newTwootContent,
        }),
        this.newTwootContent = ''
      }
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
  margin-right: 58px;
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
.user-profile_createTwoot {
  border-top: 1px solid #dfe3e8;
  padding: 20px 5px;
  display: flex;
  flex-direction: column;
}
</style>
