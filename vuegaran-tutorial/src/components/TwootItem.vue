<template>
  <div class="twoot-item" @click="favouriteTwoot(twoot.id)">
    <div class="user-profile__twoot">
      <div class="twoot-item__user">@ {{ username }}</div>
      <div class="twoot-item__content">{{ twoot.content }}</div>
    </div>
  </div>
</template>


<script>
export default {
  name: "TwootItem",
  props: {
    username: {
      type: String,
      required: true,
    },
    twoot: {
      type: Object,
      required: true,
    },
  },
  methods: {
    favouriteTwoot(id) {
      this.$emit("favourite", id);
    },
  },
};
</script>

<style>
.twoot-item {
  background-color: white;
  padding: 20px;
  margin: 0;
  border: 1px solid #dfe3e8;
  border-radius: 5px;
  box-sizing: border-box;
  cursor: pointer;
  transform: all 0.25 ease;
}

.twoot-item:hover {
  transform: scale(1.1, 1.1);
}

.twoot-item__user {
  font-weight: bold;
}
</style>
