<script setup lang="ts">
import Button from "@/components/button/Button.vue";
import {type EmitsOptions, getCurrentInstance} from "vue";

function click(a: EmitsOptions) {

}

function together() {
    for (let item of document.getElementsByClassName('a')) {
        (item as HTMLElement).click()
    }
}
function togetherMore(start: number = 0, end: number = 20) {
    requestAnimationFrame(() => {
        if (start < end) {
            start++
            together()
            setTimeout(() => {
                togetherMore(start, end)
            }, 20)
        }
    })
}
</script>

<template>
    <div class="container">
        <div>
            <Button class="a" @click="click">转圈圈！</Button>
            <br>
            <Button class="a" @click="click">长长长长长长长长长长长长长长转圈圈</Button>
            <br>
            <Button class="a" @click="click">
                超级无敌加长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长长转圈圈
            </Button>
        </div>
        <Button class="b" @click="together">一起转！</Button>
        <Button class="b" @click="togetherMore(0,50)">转很多次！</Button>
        <Button class="b" @click="togetherMore(0,1000000000000000)">根本停不下来！</Button>
    </div>
</template>
<style lang="scss" scoped>
.container {
    display: flex;
    align-items: center;
    justify-content: center;
    height: 100vh;
    flex-direction: column;

    .a,.b {
        margin-top: 50px;
    }
}
</style>