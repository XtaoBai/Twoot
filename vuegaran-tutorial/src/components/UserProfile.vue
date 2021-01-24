<template>
  <div class="user-profile">
    <div class="user-profile__user-panel">
      <h1 class="user-profile__username">@ {{ user.username }}</h1>
      <div class="user-profile__admin-badge" v-if="user.isAdmin">Admin</div>
      <div class="user-profile__admin-badge" v-else>Not Admin</div>
      <div class="user-profile__follower-count">
        <strong>Followers:</strong> {{ followers }}
      </div>
      <form class="user-profile__create-twoot" @submit.prevent="createNewTwoot">
        <label for="newTwoot"><strong>New Twoot</strong></label>
        <textarea id="newTwoot" rows="4" v-model="newTwootContent"></textarea>

        <div class="user-profile__create-twoot-type">
          <label for="newTwootType">
            <strong>Type:</strong>
          </label>
          <select id="newTwootType" v-model="selectedTwootType">
            <option
              :value="option.value"
              v-for="(option, index) in twootTypes"
              :key="index"
            >
              {{ option.name }}
            </option>
          </select>
        </div>

        <button>Twoot!</button>
      </form>
    </div>
    <div class="user-porfile__twoots-wrapper">
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
import TwootItem from "./TwootItem.vue";
export default {
  components: { TwootItem },
  name: "UserProfile",
  data() {
    return {
      newTwootContent: "",
      selectedTwootType: "instant",
      twootTypes: [
        { value: "draft", name: "Draft" },
        { value: "instant", name: "Intant Twoot" },
      ],
      followers: 0,
      user: {
        id: 1,
        username: "GaranBay",
        firstName: "Garan",
        LastName: "Bai",
        isAdmin: true,
        twoots: [
          { id: 1, content: "You are prefect!" },
          { id: 2, content: "Don't forget make yourself comfort!" },
        ],
      },
    };
  },
  computed: {
    fullName() {
      return `${this.user.firstName} ${this.user.LastName}`;
    },
  },
  mounted() {
    console.log(this.user.username);
  },
  methods: {
    followUser() {
      this.followers++;
    },
    toggleFavourite(id) {
      console.log(`Favourite Twoot #${id}`);
    },
    createNewTwoot() {
      if (this.newTwootContent && this.selectedTwootType !== "draft") {
        this.user.twoots.unshift({
          id: this.user.twoots.length + 1,
          content: this.newTwootContent,
        });
        this.newTwootContent = "";
      }
    },
  },
  watch: {
    followers(newFollowerCount, oldFollowerCount) {
      if (oldFollowerCount < newFollowerCount) {
        console.log(`${this.user.username} has gained a follower! `);
      }
    },
  },
};
</script>

<style>
.user-profile {
  display: grid;
  grid-template-columns: 1fr 3fr;
  width: 90%;
  padding: 50px 5%;
}

.user-profile__user-panel {
  display: flex;
  flex-direction: column;
  /* margin: 10px 60px 10px 0px; */
  margin-right: 50px;
  padding: 20px;
  background-color: white;
  border-radius: 5px;
  border: 1px solid #dfe3e8;
}

.user-profile__admin-badge {
  background-color: rebeccapurple;
  color: white;
  margin-top: 10px;
  border-radius: 5px;
  margin-right: auto;
  line-height: 1.5em;
  padding: 1px 10px;
  font-weight: bold;
}

.user-porfile__twoots-wrapper {
  display: grid;
  grid-gap: 14px;
}

h1 {
  margin: 0;
}

.user-profile__create-twoot {
  padding-top: 15px;
  display: flex;
  flex-direction: column;
}
</style>