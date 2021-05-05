<template>
    <form id="add">
      <input type="text" v-model="name" name="name" placeholder="player name" />
      <br>
      <input type="number" v-model="age" name="age" placeholder="player age" />
      <br>
      <input type="text" v-model="imgurl" name="imgurl" placeholder="player image" />
      <br>
      <input type="number" v-model="type" name="goals" placeholder="player goals" />
      <br>
      <input type="number" v-model="type" name="assists" placeholder="player assists" />
      <br>
      <input type="number" v-model="type" name="points" placeholder="player points" />
      <br>
      <button v-on:click=addPlayer() type="button">Add Player</button>
    </form>
</template>

<script>
export default {
    name: 'AddPlayer',
    components: {},
    data() {
        return {
            name: '',
            age: 0,
            imgurl: '',
            assists: 0,
            goals: 0,
            points: 0
        }
    },
    methods: {
        addPlayer() {
            const newPlayer = {
                name: this.name,
                age: this.age,
                imgurl: this.imgurl,
                goals: this.goals,
                assists: this.assists,
                points: this.points
            }
            this.$emit('add-player', newPlayer)
        }
    }

}
</script>

<style>


</style>