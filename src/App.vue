<template>
  <div id="app">
    <div class="wrapper">
      <h1>Simon Says</h1>
      <Board @click="handleClick" ref="board" />
      <Info
        :current="current"
        :gameover="gameover"
        :round="round"
        yar@init="startGame"
      />
      <Options @changeinterval="changeInterval" />
      <footer>
        Created by <a href="https://github.com/WotIzLove">Vlad Kurenkov</a>
      </footer>
    </div>
  </div>
</template>

<script>
import Board from "./components/Board.vue";
import Info from "./components/Info.vue";
import Options from "./components/Options.vue";

export default {
  name: "App",
  components: {
    Board,
    Info,
    Options,
  },
  data: () => ({
    layout: null,
    difficultyLevels: null,
    round: 0,
    current: 0,
    playSequence: [],
    prevButtonIdx: null,
    gameover: false,
    interval: 1500,
  }),

  methods: {
    changeInterval(interval) {
      this.interval = interval;
    },
    startGame() {
      this.round = 0;
      this.gameover = false;
      this.playSequence = [];
      this.prevButtonIdx = null;

      this.newRound();
    },

    newRound() {
      this.round += 1;
      this.current = 0;

      const idx = this.randomNumber();
      this.prevButtonIdx = idx;
      this.playSequence.push(idx);

      let i = 0;
      let idsetInterval = setInterval(() => {
        let idx = this.playSequence[i];
        this.play(idx);
        if (++i >= this.playSequence.length) {
          clearInterval(idsetInterval);
        }
      }, this.interval);
    },

    play(i) {
      this.$refs.board.$refs.button[i].animateButton();
    },

    randomNumber() {
      return Math.floor(Math.random() * 3);
    },

    handleClick(idx) {
      if (!this.round) return;

      const currentIdx = this.playSequence[this.current];

      if (idx === currentIdx) {
        setTimeout(() => this.checkWin(), 300);
      } else {
        this.gameover = true;
      }
    },

    checkWin() {
      if (this.current !== this.round - 1) {
        this.current += 1;
      } else {
        this.newRound();
      }
    },
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
  margin-top: 60px;
}

body {
  font-family: Arial, serif;
  color: #333;
  -webkit-user-select: none; /* Chrome/Safari */
  -moz-user-select: none; /* Firefox */
  -ms-user-select: none; /* IE10+ */
  -o-user-select: none;
  user-select: none;
}

h1 {
  margin: 1em 0 2em;
  text-align: center;
}

ul {
  list-style: none;
}

ul,
li {
  padding: 0;
  margin: 0;
}

p[data-action="lose"] {
  display: none;
}

.active {
  opacity: 1 !important;
}

.clearfix {
  width: 100%;
  clear: both;
}

.wrapper {
  width: 540px;
  margin: 0 auto;
}
.container {
  width: 305px;
}

.simon {
  background: #fff;
  position: relative;
  float: left;
  margin-right: 3em;
  width: 296px;
  height: 289px;
  -webkit-border-radius: 150px 150px 150px 150px;
  border-radius: 150px 150px 150px 150px;
  -moz-box-shadow: 2px 1px 12px #aaa;
  -webkit-box-shadow: 2px 1px 12px #aaa;
  -o-box-shadow: 2px 1px 12px #aaa;
  box-shadow: 2px 1px 12px #aaa;
}

.tile {
  opacity: 0.6;
  outline: none;
  -webkit-transition: opacity 250ms ease;
  -moz-transition: opacity 250ms ease;
  -ms-transition: opacity 250ms ease;
  -o-transition: opacity 250ms ease;
  transition: opacity 250ms ease;
}

.tile.lit {
  opacity: 1;
}

.red,
.blue,
.yellow,
.green {
  height: 290px;
  -webkit-border-radius: 150px 150px 150px 150px;
  border-radius: 150px 150px 150px 150px;
  position: absolute;
  text-indent: 10000px;
}

.red:hover,
.blue:hover,
.yellow:hover,
.green:hover {
  border: 2px solid black;
}

.red {
  background: #ff5643;
  clip: rect(0px, 300px, 150px, 150px);
  width: 296px;
}

.blue {
  background: dodgerblue;
  clip: rect(0px, 150px, 150px, 0px);
  width: 300px;
}

.yellow {
  background: #feef33;
  clip: rect(150px, 150px, 300px, 0px);
  width: 300px;
}

.green {
  background: #bede15;
  clip: rect(150px, 300px, 300px, 150px);
  width: 296px;
}

.game-info {
  margin-top: 90px;
}

.game-info button {
  width: 5em;
  box-sizing: border-box;
  font-size: 1.4em;
  -webkit-border-radius: 10px 10px 10px 10px;
  border-radius: 10px 10px 10px 10px;
  background: #6dabe8;
  border: none;
  padding: 0.3em 0.6em;
}

.game-info button:hover {
  background: #78bcff;
}

.game-options h2 {
  margin-top: 30px;
  margin-bottom: 0;
}

.game-options input[type="radio"] {
  margin-right: 10px;
}

.hoverable:hover {
  cursor: pointer;
}

.simon-template {
  position: absolute;
}

footer {
  position: absolute;
  bottom: 20px;
  width: 540px;
  clear: both;
  text-align: center;
}
</style>
