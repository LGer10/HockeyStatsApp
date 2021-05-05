<template>
  <form>
    <h2>Add other Player</h2>
    <hr>
    <b-form-input :state="null" 
    type="text" 
    v-model="name" 
    name="name" 
    placeholder="player name" />
    <br />
    <b-form-input :state="null"
      type="text"
      v-model="imgurl"
      name="imgurl"
      placeholder="player image"
    />
    <br />
    <b-form-input :state="null" 
      type="number"
      v-model="goals"
      name="goals"
      placeholder="player goals"
    />
    <br />
    <b-form-input :state="null"
      type="number"
      v-model="assists"
      name="assists"
      placeholder="player assists"
    />
    <br />
   
    <b-button variant="primary" v-on:click="addPlayer()" type="button">Add Player</b-button>
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
