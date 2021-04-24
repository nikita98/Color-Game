<template>
  <div class="timer">прошло {{ time }}</div>
</template>

<script>
export default {
  data() {
    return {
      isStart: false,
      time: "0",
      startTime: "",
    };
  },
  methods: {
    start() {
      this.isStart = true;
      this.startTime = new Date();
      setInterval(() => {
        if (this.isStart) {
          this.updateTime();
        }
      }, 50);
    },
    stop: function () {
      this.isStart = false;
    },
    win() {
      this.stop();
      this.$emit("writeTime", this.time);
    },
    updateTime: function () {
      const pad = (digit) => digit.toString().padStart(2, "0");
      const today = new Date() - this.startTime,
        minutes = Math.floor(today / 36000),
        seconds = Math.floor((today % 36000) / 600),
        milliSeconds = today % 600;
      this.time = `${pad(minutes)}:${pad(seconds)}:${pad(
        Math.floor(milliSeconds / 10)
      )}`;
    },
  },
};
</script>

<style scoped lang="scss">
</style>
