<template>
  <form>
    <h2>Add custom Player</h2>
    <hr>
      <b-form-group  label="Name" label-for="name">
    <b-form-input 
    id="name"
    type="text" 
    v-model="name" 
    name="name" 
    placeholder="player name" />
        </b-form-group>

    <br />
      <b-form-group label="Image URL" label-for="imgurl" >
    <b-form-input 
    id="imgurl"
      type="text"
      v-model="imgurl"
      name="imgurl"
      placeholder="player image"
    />
      </b-form-group>

    <br />
    <b-form-group label="Goals" label-for="goals">
    <b-form-input  
      id="goals"
      type="number"
      v-model="goals"
      name="goals"
      placeholder="player goals"
    />
    </b-form-group>

    <br />
     <b-form-group  label="Assissts" label-for="assists">
    <b-form-input 
    id="assists"
      type="number"
      v-model="assists"
      name="assists"
      placeholder="player assists"
    />
        </b-form-group>

    <br />
   
    <b-button variant="outline-primary" v-on:click="addPlayer()" type="button">Add Player</b-button>
  </form>
</template>

<script>
export default {
  name: "AddPlayer",
  components: {},
  data() {
    return {
      
    };
  },
  methods: {
    addPlayer() {
      const newPlayer = {
        name: this.name,
        imgurl: this.imgurl,
        goals: this.goals,
        assists: this.assists,
      };
      this.$emit("add-player", newPlayer);
    },
  },
};
</script>
