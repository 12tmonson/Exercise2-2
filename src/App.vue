<template>
  <div id="app">
<head>
  <title>RPS with VueJS</title>
  <link href="css/foundation.min.css" rel="stylesheet">
  <link href="css/app.css" rel="stylesheet">
  <link href="https://cdnjs.cloudflare.com/ajax/libs/foundation/6.4.3/css/foundation.min.css" rel="stylesheet">
</head>


  <section class="row">
    <div class="small-6 columns">
      <h1 class="text-center">PLAYER</h1>
      <div class="wins">
        <div :style="{ width: (playerWins * 10) + '%' }" class="wins text-center" style="background-color: green; margin: 0; color: white;">
          {{ playerWins }}
        </div>
      </div>
    </div>
    <div class="small-6 columns">
      <h1 class="text-center">COMPUTER</h1>
      <div class="wins">
        <div :style="{ width: (computerWins * 10) + '%' }" class="wins text-center" style="background-color: green; margin: 0; color: white;">
          {{ computerWins }}
        </div>
      </div>
    </div>
  </section>
  <section v-if="!gameIsRunning" class="row controls">
    <div class="small-12 columns">
      <button id="start-game" @click="startGame">START NEW GAME</button>
    </div>
  </section>
  <section v-else class="row controls">
    <div class="small-12 columns">
      <button id="rock" @click="rockUser">ROCK</button>
      <button id="paper" @click="paperUser">PAPER</button>
      <button id="rock" @click="scissorsUser">SCISSORS</button>

    </div>
  </section>
  <section v-if="turns.length > 0" class="row log">
    <div class="small-12 columns">
      <ul>
        <li v-for="turn in turns" :key="turn" :class="{'player-turn': turn.isPlayer, 'computer-turn': !turn.isPlayer, 'tie-turn': turn.tie}">
              {{ turn.text }}
        </li>
      </ul>
    </div>
  </section>
</div>



</template>

<script>
export default {

  el: '#app',
  data() {
    return {
    playerWins: 0,
    computerWins: 0,
    gameIsRunning: false,
    rock: 1,
    paper: 2,
    scissors: 3,
    turns: []
  }
  },
  methods: {
    startGame () {
      this.gameIsRunning = true;
      this.playerWins = 0;
      this.computerWins = 0;
      this.turns = [];
    },
    rockUser () {
      let computerChoice = this.calculateComputerChoice();

      if (computerChoice === this.paper) {
        this.computerWins += 1;
        this.turns.unshift({
          isPlayer: false,
          text: 'Computer Chose Paper | Paper Beats Rock | Computer Wins!'
        });
      } else if (computerChoice === this.scissors) {
        this.playerWins += 1;
        this.turns.unshift({
          isPlayer: true,
          text: 'Computer Chose Scissors | Rock Beats Scissors | Player Wins!'
        });
      } else {
        this.turns.unshift({
          tie: true,
          text: 'Computer Chose Rock | You Have Tied!'
        });
      }
    },
    calculateComputerChoice () {
      let max = 3;
      let min = 0;

      return Math.max(Math.floor(Math.random() * max) + 1, min);
    }
  }};

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.text-center {
    text-align: center;
}

.wins {
    width: 80%;
    color: black;
    height: 40px;
    background-color: #eee;
    margin: auto;
    transition: width 1000ms;
}

.controls, .log {
    margin-top: 30px;
    text-align: center;
    padding: 10px;
    border: 1px solid #ccc;
    box-shadow: 0px 3px 6px #ccc;
}

.turn {
    margin-top: 20px;
    margin-bottom: 20px;
    font-weight: bold;
    font-size: 22px;
}

.log ul {
    list-style: none;
    font-weight: bold;
    text-transform: uppercase;
}

.log ul li {
    margin: 5px;
}

.log ul .player-turn {
    color: green;
    background-color: #aaffb0;
}

.log ul .computer-turn {
    color: red;
    background-color: #ffc0c1;
}

.log ul .tie-turn {
  color: blue;
  background-color: #e4e8ff;
}

button {
    font-size: 20px;
    background-color: #eee;
    padding: 12px;
    box-shadow: 0 1px 1px black;
    margin: 10px;
}

#start-game {
    background-color: #e4e8ff;
}

#start-game:hover {
  background-color: #687eff;
}

#rock {
    background-color: #ff7367;
}

#rock:hover {
    background-color: #ff3f43;
}

#paper {
    background-color: #ffaf4f;
}

#paper:hover {
    background-color: #ff9a2b;
}

#scissors {
    background-color: #aaffb0;
}

#scissors:hover {
    background-color: #76ff7e;
}

#restart {
    background-color: #ffffff;
}

#restart:hover {
    background-color: #c7c7c7;
}
</style>
