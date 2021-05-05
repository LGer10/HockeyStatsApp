<template>
  <div id="app">
    <Header  />
    <div class="container-fluid">
      <b-button variant="primary"
      v-b-toggle.collapseData class="m-1" type="button">
        Display All Stats</b-button>
      <b-collapse id="collapseData">
        <b-table hover striped :items="apiData"> </b-table>
      </b-collapse>
      <div class="row">
        <div class="col-md-3 border align-items-center">
          <h2>Favourite Players</h2>
          <hr />
          <span v-if="loading">Loading...</span>
          <table v-for="player in players" :key="player.points">
            <b-card
              :title="player.name"
              :img-src="player.imgurl"
              img-alt="Image"
              img-top
              border-variant="light"
              
            >
              <b-card-text>
                <br />
                <p style="font-size: 14pt">
                  Goals: {{ player.goals }}
                </p>
                <p style="font-size: 14pt">Assists: {{ player.assists }}</p>
              
                <p style="font-size: 20pt; font-weight: bold">
                  Points: {{ player.assists + player.goals }}
                </p>
                <form>
                  <b-collapse id="collapse">
                    <b-input
                      type="number"
                      v-model="goals"
                      name="goals"
                      placeholder="player goals"
                    />
                    <b-input
                      type="number"
                      v-model="assists"
                      name="assists"
                      placeholder="player assists"
                    />
                    <b-input
                      type="text"
                      v-model="imgurl"
                      name="img"
                      placeholder="player image-url"
                    />
                    <b-button
                      variant="outline-success"
                      v-b-toggle.collapse
                      class="m-1"
                      type="button"
                      v-on:click="updatePlayer(player._id, player)"
                      >save</b-button
                    >
                  </b-collapse>
                </form>
                <b-button variant="outline-primary" v-b-toggle.collapse class="m-1" type="button">
                  <b-icon icon="pencil-square"></b-icon>
                </b-button>
&nbsp;&nbsp;
                <b-button
                  variant="outline-danger"
                  id="delete"
                  v-on:click="deletePlayer(player._id)"
                  type="button"
                >
                  &#x2717;
                </b-button>

                <br />
              </b-card-text>
            </b-card>
          </table>
        </div>

        <br />
        <div class="col-md-6 border">
            <h2>Players</h2>
          <hr />

          <input type="text" placeholder="search by name" v-model="filter" />

          <b-button variant="outline-primary"
          v-b-toggle.collapsePlayers class="m-1" type="button">
            <b-icon icon="search"></b-icon
          ></b-button>

          <b-collapse id="collapsePlayers">
            <table>
              <thead>
                <tr>
                  <th>Name</th>
                  <th>Team</th>
                  <th>Position</th>
                  <th>Games</th>
                  <th>Season</th>
                  <th>G</th>
                  <th>A</th>
                  <th>PPG</th>
                  <th>SHG</th>
                  <th>SOG</th>
                  <th></th>

                </tr>
              </thead>
              <tbody>
                <tr v-for="item in filteredItems" :key="item.PlayerID">
                  <td style="font-weight: bold">{{ item.Name }}</td>
                  <td>{{ item.Team }}</td>
                  <td>{{ item.Position }}</td>
                  <td>{{ item.Games }}</td>
                  <td>{{ item.Season }}</td>
                  <td>{{ float2int(item.Goals) }}</td>
                  <td>{{ float2int(item.Assists) }}</td>
                  <td>{{ float2int(item.PowerPlayGoals) }}</td>
                  <td>{{ float2int(item.ShortHandedGoals) }}</td>
                  <td>{{ float2int(item.ShotsOnGoal) }}</td>

                  
                    <b-button
                      variant="outline-light"
                      v-on:click="loadPlayer(`${item.PlayerID}`)"
                      type="button"
                      ><b-icon icon="plus-circle" variant="primary"></b-icon>
                    </b-button>
                 
                </tr>
              </tbody>
            </table>
          </b-collapse>
          <br>
                    <br>

          <img id="alex" src="./assets/ovi.jpg">
        </div>
        <div class="col-md-3 border">
          <AddPlayer v-on:add-player="addPlayer" />
        </div>
      </div>
    </div>

    <br />
    <hr />
  </div>
</template>

<script>
import axios from "axios";
import Header from "./components/Header";
import AddPlayer from "./components/AddPlayer";

const baseUrl = "https://nhlplayers-f568.restdb.io/rest/players";
const apiURL = "https://fly.sportsdata.io/v3/nhl/stats/json/PlayerSeasonStats/2021?key=8179b11fe5a34375ad15357802d5bd34";
const config = {
  async: true,
  crossDomain: true,
  headers: {
    "content-type": "application/json",
    "x-apikey": "605db82c358add1705bd17d2",
    "cache-control": "no-cache",
  },
};
export default {
  name: "App",
  components: {
    Header,
    AddPlayer,
  },
  data() {
    return {
      players: [],
      apiData: [],
      loading: false,
      playerData: null,
      filter: "",
    };
  },

  methods: {
    float2int(value) {
      return value | 0;
    },
    async getPlayer() {
      this.loading = true;
      try {
        let response = await axios.get(baseUrl, config);
        this.players = response.data;
        console.log(this.players);
      } catch (error) {
        console.log(`Cant load player. Error: ${error}`);
      }
      this.loading = false;
    },

    async addPlayer(newPlayer) {
      try {
        await axios.post(baseUrl, newPlayer, config);
      } catch (error) {
        console.log(`Cant add player. Error: ${error}`);
      }
      this.players.push(newPlayer);
    },

    async updatePlayer(id) {
      const player = {
        goals: this.goals,
        assists: this.assists,
        points: this.points,
        imgurl: this.imgurl,
      };
      try {
        await axios.put(`${baseUrl}/${id}`, player, config);
      } catch (error) {
        console.log(`Cant update player. Error: ${error}`);
      }
    },
    async deletePlayer(id) {
      try {
        await axios.delete(`${baseUrl}/${id}`, config);
      } catch (error) {
        console.log(`Cant delete player. Error: ${error}`);
      }
      let currentIndex = this.players.findIndex((player) => player._id === id);
      this.players.splice(currentIndex, 1);
    },
async getApiData() {
      try {
        axios.get(apiURL).then((response) => (this.apiData = response.data));
      } catch (error) {
        console.log(`Cant get data. Error: ${error}`);
      }
    },
    

    async loadPlayer(id) {
      var playerUrl = `https://fly.sportsdata.io/v3/nhl/stats/json/PlayerSeasonStatsByPlayer/2021/${id}?key=8179b11fe5a34375ad15357802d5bd34`;
      try {
        await axios
          .get(playerUrl)
          .then((response) => (this.playerData = response.data));
      } catch (error) {
        console.log(`Cant add player. Error: ${error}`);
      }
     const newPlayer = {
        name: this.playerData.Name,
        goals: this.float2int(this.playerData.Goals),
        assists: this.float2int(this.playerData.Assists),
        imgurl: "https://us.123rf.com/450wm/kapona/kapona1703/kapona170300020/73251908-hockey-spieler-illustration.jpg?ver=6"
      };

            this.addPlayer(newPlayer);

    },
  },
  computed: {
    filteredItems() {
      return this.apiData.filter((item) => {
        return item.Name.toLowerCase().indexOf(this.filter.toLowerCase()) > -1;
      });
    },
  },

  created() {
    this.getPlayer();
    this.getApiData();
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
h2 {
  padding-top: 10px ;
}
#delete {
  color: red;
}

#alex {
  border-radius: 5px;
  margin: 0 auto;
}

tr:nth-child(even) {
  background-color: #f2f2f2;
}

table {
  width: 100%;
  margin: 0 auto;
}

th {
  background-color: lightgrey;
  font-size: 14pt;
}
</style>
