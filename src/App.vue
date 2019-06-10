<template>
  <div class="game">
    <div class="game__inner">
      <div class="game__grid">
        <div
          class="game__grid-item"
          v-for=" item in grid"
          :key="item"
          @click="selectElem($event)"
        ></div>
      </div>
      <button class="game__button">Старт</button>
      <div class="timer">00:00:00</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "app",
  data() {
    return {
      number: 24,
      colors: [],
      first: false,
      second: false,
      animation: false,
      grid: []
    };
  },

  created() {
		this.creatgrid();
    this.notRandomColors();
  },

  methods: {
    creatgrid() {
      for (let i = 0; i < this.number; i++) {
        this.grid[i] = i;
			}
			console.log(this.grid);
    },
    notRandomColors() {
      let colorsCol = this.number / 2,
        radix = 0,
        colorsTemplate = [];

      while (radix * radix * radix < colorsCol) {
        radix++;
      }

      createColorsTemplate();
			createColors(this.colors);
			randomColors(this.colors);
			fillGrid(this.colors, this.grid);

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
            colors[i][j] = Math.floor((255 / 2) * colorsTemplate[i][j]);
          }
        }
      }

      function randomColors(colors) {
        colors = colors.concat(colors);
        function compareRandom(a, b) {
          return Math.random() - 0.5;
        }
        colors.sort(compareRandom);
        colors.sort(compareRandom);
      }

      function fillGrid(colors, grid) {
							
			}
    },

    selectElem(event) {
      if (!this.animation) {
        if (!this.first) {
          this.first = event.target;
          this.first.classList.add("active");
        } else {
          this.second = event.target;
          this.second.classList.add("active");
          if (this.first) {
            let that = this;
            this.animation = true;
            setTimeout(function() {
              that.first.classList.remove("active");
              that.second.classList.remove("active");
              that.animation = false;
            }, 1000);
          }
        }
      }
    }
  }
};
</script>

<style scoped lang="scss">
.game {
  box-sizing: border-box;
  width: 500px;
  margin: 20px auto;
  padding: 15px;
  background-color: #b1cde0;
  &__grid {
    width: 100%;
    display: flex;
    flex-wrap: wrap;
    background-color: #fff;
    border: 1px solid #0998b8;
    margin-bottom: 30px;
  }
  &__grid-item {
    box-sizing: border-box;
    position: relative;
    width: 25%;
    height: 100px;
    border: 1px solid #0998b8;
    background-color: #abbfd4;

    &:after {
      content: "";
      position: absolute;
      height: 100%;
      width: 100%;
      background-color: #fff;
      left: 0;
      top: 0;
      transition: 0.5s;
    }
    &.active:after {
      background-color: rgba(#fff, 0);
    }
    &.finished:after {
      background-color: rgba(#fff, 0);
      border: 1px sloid #ffc0cb;
    }
  }
}
</style>
