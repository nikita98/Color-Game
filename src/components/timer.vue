<template>
    <div class="timer">
        прошло {{time}}
    </div>
</template>

<script>
    export default {
        data() {
            return {
                time: '',
                startTime: ''
            };
        },
        methods: {
            start: function () {
                this.updateTime();
            },
            updateTime: function () {
                const pad = digit =>
                    digit.toString().padStart(2, '0');
                const today = new Date(),
                    minutes = today.getMinutes(),
                    seconds = today.getSeconds(),
                    milliSeconds = today.getMilliseconds();
                this.time = `${pad(minutes)}:${pad(seconds)}:${pad(Math.floor(milliSeconds / 10))}`
            }
        },
        created: function () {
            setInterval(() => this.start(), 100);
            this.startTime = new Date();
        }
    };
</script>

<style scoped lang="scss">
</style>
