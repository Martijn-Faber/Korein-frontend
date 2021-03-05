<template>
<div v-if="this.status">
  <Overlay :overlayActive="state === 'prepare'"></Overlay>
  <h1 v-if="winner.length > 1">{{ winner }}!</h1>
  <p>Jullie waren {{ delta.differce }} {{ delta.units }} sneller als {{ loser }}</p>
  <div>
    <h4>{{ status[0].name }}</h4>
    <h1>{{ status[0].time }} secondes</h1>
  </div>
  <div>
    <h4>{{ status[1].name }}</h4>
    <h1>{{ status[1].time }} secondes</h1>
  </div>
</div>
</template>

<script>
import Overlay from '../components/Overlay';
export default {
  name: 'HelloWorld',
  components: {
    Overlay
  },
  data() {
    return {
      status: Object,
      winner: String,
      loser: String,
      differce: Object,
      state: "prepare"
    }
  },
  methods: {
    getStatus: async function() {
      let response = await fetch('http://localhost:5000/api/getstatus', {
        mode: 'cors',
      });

      if (response.ok) {
        let json = await response.json();
        this.status = json
        this.checkWinner()
      } else {
        alert("HTTP-Error: " + response.status);
      }
    },
    checkWinner: function(){
      if (this.status[0].time < this.status[1].time) {
        this.winner = `Goed gedaan ${this.status[0].name}`
        this.loser = this.status[1].name
      } else if (this.status[1].time < this.status[0].time) {
        this.winner = `Goed gedaan ${this.status[1].name}`
        this.loser = this.status[0].name
      } else if (this.status[0].time === this.status[1].time) {
        this.winner = "Goed gedaan jullie hebben beide gewonnen!"
      } else {
        console.log("Foutje moe kunnen")
        this.winnen = ""
      }
      this.checkDifference()
    },
    checkDifference: function() {
      let difference = Math.abs(this.status[1].time - this.status[0].time)

      console.log(difference)
      
      this.delta = {
        differce: difference.toString(),
        units: "secondes"
      }

      if (difference === 1) {
        this.delta.units = "seconde"
      } else if (difference < 1) {
        this.delta.units = "miliseconde"
        this.delta.differce = Math.round(difference * 1000)
      } else {
        this.delta.differce = Math.round(difference * 100)/100
      }

      this.differce.units
    }
  },
  mounted() {
    this.getStatus()
  },
}
</script>

<style scoped>
Overlay {
    z-index: 100;
}
</style>
