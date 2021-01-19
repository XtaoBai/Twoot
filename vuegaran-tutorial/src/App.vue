<template>
  <div class="app">
    @{{user.username}} - {{ fullName }}
    <strong>Followers:</strong>
    {{followers}}
    <button @click="followUser">Follow</button>
  </div>

</template>

<script>


export default {
  name: 'App',
  data(){
    return{
      followers: 0,
      user:{
        id: 1,
        username: 'GaranBay',
        firstName: 'Garan',
        LastName: 'Bai',
        isAdmin: true
      }
    }
  },
  computed:{
    fullName(){
      return `${this.user.firstName} ${this.user.LastName}`
    }
  },
  mounted(){
    console.log(this.user.username)
  },
  methods:{
    followUser(){
      this.followers++
    }
  },
  watch:{
    followers(newFollowerCount, oldFollowerCount){
      if (oldFollowerCount < newFollowerCount){
        console.log(`${this.user.username} has gained a follower! `)
      }
    }
  }
  
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  min-height: 100vh;
  background-color: #F3F5FA;
}
</style>
