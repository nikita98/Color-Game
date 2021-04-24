<template>
  <div class="leaderboard">
    <div class="leaderboard__title">Лучшее время</div>
    <div
      class="leaderboard__item"
      v-for="(item, index) in winners"
      :key="item.index"
    >
      {{ winners[index] }}
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      winners: ["05.00.00"],
    };
  },
  methods: {
    addWinner: function (time) {
      this.winners.push(time);
    },
  },
};
</script>

<style>
</style>