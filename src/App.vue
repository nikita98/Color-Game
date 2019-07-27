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
            <button class="game__button">Старт</button>
            <div class="timer">00:00:00</div>
        </div>
    </div>
</template>

<script>
    import gridItem from './components/grid-item.vue';
    import GridItem from "./components/grid-item";

    export default {
        name: "app",
        components: {GridItem},
        data() {
            return {
                number: 24,
                first: false,
                second: false,
                animation: false,
                grid: []
            };
        },

        created() {
            this.notRandomColors();
        },
        comments: {
            gridItem
        },
        methods: {
            notRandomColors() {
                let colors = [],
                    colorsCol = this.number / 2,
                    radix = 0,
                    colorsTemplate = [];

                while (radix * radix * radix < colorsCol) {
                    radix++;
                }
                while (radix * radix * radix < colorsCol) {
                    radix++;
                }

                createColorsTemplate();
                createColors(colors);
                colors = randomColors(colors);
                createGrid(colors, this.grid);

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
                            colors[i][j] = (Math.floor((255 / (radix - 1))) * colorsTemplate[i][j]);
                        }
                    }
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

                function createGrid(colors, grid) {
                    for (let i = 0; i < colors.length; i++) {
                        grid[i] = {index: i, color: "#"};
                        for (let j = 0; j < colors[j].length; j++) {
                            let color = colors[i][j].toString(16);
                            grid[i].color += (color.length < 2 ? color + color : color)
                            // grid[i] += (colors[i][j].toString(16) ? colors[i][j].toString(16) : "00");
                        }
                    }
                }
            },
            selectElem() {
                if (!this.animation) {
                    if (!this.first) {
                        this.first = event.target;
                        this.first.classList.add("active");
                    } else {
                        this.second = event.target;
                        this.second.classList.add("active");
                        this.animation = true;
                        let that = this;
                        // console.log(this.first.style.backgroundColor);
                        // console.log(this.second);
                        setTimeout(function () {
                            that.first.classList.remove("active");
                            that.second.classList.remove("active");
                            if (that.first.style.backgroundColor === that.second.style.backgroundColor) {
                                that.first.classList.add("finished");
                                that.second.classList.add("finished");
                            }
                            that.first = "";
                            that.second = "";
                            that.animation = false;
                        }, 1000);
                    }
                }
            }
        }
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
            margin-bottom: 30px;
        }
    }
</style>

