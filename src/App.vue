<template>
  <div class="game">
    <div class="game__grid">
      <grid-item
        v-for="item in grid"
        :key="item.index"
        :color="item.color"
        @selectElem="selectElem($event)"
      ></grid-item>
    </div>
    <div class="game__start">
      <timer ref="timer" v-on:writeTime="writeTime" />
      <div class="items-col">
        <div class="items-col__num">{{ number }}</div>
        <button class="items-col__action" @click="numPlus()">+</button>
        <button class="items-col__action" @click="numMinus()">-</button>
      </div>
      <button class="game__button" @click="gameStart()">Старт</button>
      <button class="game__button" @click="gameEnd()">Стоп</button>
    </div>
    <leaderboard ref="leaderboard" />
  </div>
</template>

<script>
import gridItem from "./components/grid-item.vue";
import timer from "./components/timer.vue";
import leaderboard from "./components/leaderboard.vue";

export default {
  data() {
    return {
      start: false,
      number: 16,
      remained: 16,
      first: false,
      second: false,
      animation: false,
      grid: [],
      colors: [],
    };
  },
  components: {
    gridItem,
    timer,
    leaderboard,
  },
  methods: {
    gameStart() {
      if (!this.start) {
        this.colors = [];
        this.grid = [];
        this.remained = this.number;
        this.first = false;
        this.second = false;
        this.notRandomColors();
        this.start = true;
        this.$refs.timer.start();
      } else {
        this.gameEnd();
        setTimeout(this.gameStart, 0);
      }
    },
    gameEnd() {
      this.grid = this.grid.slice(1, 1);
      this.start = false;
      this.$refs.timer.stop();
    },
    notRandomColors() {
      let colorsCol = this.number / 2,
        radix = 0,
        colorsTemplate = [];

      createRadix();
      createColorsTemplate();
      this.colors = createColors(this.colors);
      this.colors = randomColors(this.colors);
      this.grid = fillGrid(this.colors);

      function createRadix() {
        while (radix * radix * radix < colorsCol) {
          radix++;
        }
      }

      function createColorsTemplate() {
        for (let i = 0; i < colorsCol; i++) {
          colorsTemplate[i] = "";
          let one = Math.floor(i / (radix * radix)),
            two = Math.floor((i - one * radix * radix) / radix),
            three = i - one * radix * radix - two * radix;
          colorsTemplate[i] += one;
          colorsTemplate[i] += two;
          colorsTemplate[i] += three;
        }
      }

      function createColors(colors) {
        for (let i = 0; i < colorsCol; i++) {
          colors[i] = [];
          for (let j = 0; j < 3; j++) {
            // let color = ((Math.floor((185 / (radix - 1))) * colorsTemplate[i][j]) + 85);
            // colors[i][j] = color < 255 ? color : 255;
            colors[i][j] = Math.floor(255 / (radix - 1)) * colorsTemplate[i][j];
          }
        }
        return colors;
      }

      function randomColors(colors) {
        colors = colors.concat(colors);

        function compareRandom() {
          return Math.random() - 0.5;
        }

        colors.sort(compareRandom);
        colors.sort(compareRandom);
        return colors;
      }

      function fillGrid(colors) {
        let grid = [];
        for (let i = 0; i < colors.length; i++) {
          grid[i] = { index: i, color: "#" };
          for (let j = 0; j < colors[j].length; j++) {
            let color = colors[i][j].toString(16);
            grid[i].color += color.length < 2 ? color + color : color;
          }
        }
        return grid;
      }
    },
    selectElem() {
      if (!this.animation && this.start) {
        if (!this.first) {
          this.first = event.target;
          this.first.classList.add("active");
        } else if (this.first !== event.target) {
          this.second = event.target;
          this.second.classList.add("active");
          this.animation = true;
          let that = this;
          setTimeout(function () {
            that.first.classList.remove("active");
            that.second.classList.remove("active");
            if (
              that.first.style.backgroundColor ===
              that.second.style.backgroundColor
            ) {
              that.first.classList.add("finished");
              that.second.classList.add("finished");
              that.remained -= 2;
            }
            that.first = "";
            that.second = "";
            that.animation = false;
            if (!that.remained) {
              that.win();
            }
          }, 300);
        }
      }
    },
    win() {
      this.$refs.timer.win();
    },
    writeTime(time) {
      // console.log(this.$refs.leaderboard);
      // this.$refs.leaderboard.winners.push(time);
      // console.log(this.$refs.leaderboard.winners);
      this.$refs.leaderboard.addWinner(time);
    },
    numPlus() {
      if (!this.start) {
        this.number += 4;
      }
    },
    numMinus() {
      if (!this.start) {
        this.number -= 4;
      }
    },
  },
};
</script>

<style lang="scss">
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

.game {
  background-color: #b1cde0;
  display: flex;

  &__grid {
    width: 450px;
    height: 100vh;
    display: flex;
    flex-wrap: wrap;
    background-color: #fff;
    border: 1px solid #0998b8;
  }
}
</style>

