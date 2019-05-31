<template>
  <div class="game">
    <div class="game__inner">
      <div class="game__grid">
        <!-- Сдаюсь, не могу понять, как мне отправить обьект Vue и приделать к нему класс.. -->
        <div
          class="game__grid-item"  
          :class="{ active: isActive }"
          v-for="(item, index) in grid"
          :key="index"
          @click="selectElem(item, index)"
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
      isActive: false,
      grid: []
    };
  },
  created() {
    this.creatgrid();
  },
  methods: {
    creatgrid() {
      for (let i = 0; i < 16; i++) {
        this.grid[i] = false;
      }
    },
    selectElem(item, index) {
      console.log(item, index);
      console.log(this);
    }
  }
  // components: {}
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
    width: 25%;
    height: 100px;
    border: 1px solid #0998b8;
  }
}
</style>
