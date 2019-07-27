<template>
    <div :style="{'background-color': color}"
         class="grid-item"
         @click="itemClick"
    ></div>
</template>

<script>
    export default {
        props: {
            color: {
                type: String,
                default: "#000000"
            }
        },
        data() {
            return {
                active: false,
                finished: false
            };
        },
        methods: {
            itemClick() {
                this.$emit('selectElem')
            }
        }
    };
</script>

<style scoped lang="scss">
    .grid-item {
        position: relative;
        width: 25%;
        border: 1px solid #04847f;
        background-color: #abbfd4;

        &:after {
            content: "";
            position: absolute;
            height: 100%;
            width: 100%;
            left: 0;
            top: 0;
            background-color: rgba(#fff, 1);
            transition: 0.5s;
        }

        &.active:after {
            background-color: rgba(#fff, 0);
        }

        &.finished:after {
            background-color: rgba(#fff, 0);
        }

        &:before {
            content: "";
            position: absolute;
            height: 100%;
            width: 100%;
            left: 0;
            top: 0;
            background-color: rgba(#d8d, 0.2);
        }
    }
</style>
