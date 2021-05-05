<template>
  <div id="app">

    <Header />
         
    <img align="left" alt="alex pic" src="./assets/ovi.jpg" />

    <Main align="middle"/>
     <AddPlayer align="middle" v-on:add-player="addPlayer" />
     <hr>
    <span v-if="loading">Loading...</span>
    <ul>
      <li v-for="player in players" :key="player.id">
        {{ player.name }}, age {{ player.age }} <br>
        Goals: {{ player.goals }}
        Assists: {{ player.assists }}
        Points: {{ player.points }}   
        <button id="delete" v-on:click="deletePlayer(player._id)" type="button">&#x2717;</button>
        <br>
        <br>
      </li>
    </ul>

    
  </div>
</template>

<script>
import axios from 'axios'
import Header from './components/Header'
import Main from './components/Main'
import AddPlayer from './components/AddPlayer'

const baseUrl = 'https://nhlplayers-f568.restdb.io/rest/players'
const config = {
  async: true,
  crossDomain: true,
  headers: {
    'content-type': 'application/json',
    'x-apikey': '605db82c358add1705bd17d2',
    'cache-control': 'no-cache'
  }
}

export default {
  name: 'App',
  components: {
    Header,
    Main,
    AddPlayer,
  },
  data() {
    return {
      player: [],
      loading: false,
    }
  },
  methods: {
    async getPlayer() {
      this.loading = true
      try {
        let response = await axios.get(baseUrl, config)
        this.players = response.data
        console.log(this.players)
      } catch(error) {
        console.log(`Cant load pets. Error: ${error}`)
      }
      this.loading = false
    },
    async addPlayer(newPlayer) {
      try {
        await axios.post(baseUrl, newPlayer, config)
      } catch (error) {
        console.log(`Cant add player. Error: ${error}`)
      }
      this.players.push(newPlayer)
    },
    async deletePlayer(id) {
      try {
        await axios.delete(`${baseUrl}/${id}`, config)
      } catch (error) {
        console.log(`Cant delete pet. Error: ${error}`)
      }
      let currentIndex = this.player.findIndex(player => player._id === id)
      this.players.splice(currentIndex, 1)
    }
  },
  created() {
    this.getPlayer()
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
  margin-top: 20px;
}
#delete {
  color: red;

}
</style>
