<template>
  <div class="user-profile">
    <div class="user-profile__sidebar">
      <div class="user-profile__user-panel">
        <h1 class="user-profile__username">@{{ user.username }}</h1>
        <div class="user-profile__admin-badge" v-if="user.isAdmin">Admin</div>
        <div class="user-profile__follower-count">
          <strong>Followers: </strong> {{ followers }}
        </div>
      </div>
      <CreateTwootPanel @add-twoot="addTwoot" />
    </div>
    <div class="user-profile__twoots-wrapper">
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
import TwootItem from "../components/TwootItem";
import CreateTwootPanel from "../components/CreateTwootPanel";
export default {
  name: "UserProfile",
  components: { TwootItem, CreateTwootPanel },
  data() {
    return {
      followers: 0,
      user: {
        id: 1,
        username: "GaranBay",
        firstName: "Garan",
        LastName: "Bai",
        email: "GaranBay@163.com",
        isAdmin: true,
        twoots: [
          { id: 1, content: "You are prefect!" },
          { id: 2, content: "Don't forget make yourself comfort!" },
        ],
      },
    };
  },

  methods: {
    toggleFavourite(id) {
      console.log(`Favourite Twoot #${id}`);
    },
    addTwoot(newTwootContent) {
      this.user.twoots.unshift({
        id: this.user.twoots.length + 1,
        content: newTwootContent,
      });
    },
  },
};
</script>

<style lang='scss' scoped>
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  grid-gap: 50px;
  padding: 50px 5%;

  .user-profile__user-panel {
    display: flex;
    flex-direction: column;
    // margin-right: 50px;
    padding: 20px;
    background-color: white;
    border-radius: 5px;
    border: 1px solid #dfe3e8;
    margin-bottom: auto;

    h1 {
      margin: 0;
    }

    .user-profile__admin-badge {
      background: rebeccapurple;
      color: white;
      margin-top: 10px;
      border-radius: 5px;
      margin-right: auto;
      line-height: 1.5em;
      padding: 1px 10px;
      font-weight: bold;
    }
  }

  .user-profile__twoots-wrapper {
    display: grid;
    grid-gap: 14px;
    margin-bottom: auto;
  }
}
</style>