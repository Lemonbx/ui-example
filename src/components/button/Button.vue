<script setup lang="ts">
import hertaa1 from '@/assets/img/hertaa1.gif'
import hertaa2 from '@/assets/img/hertaa2.gif'
import gululu from '@/assets/audio/gululu.mp3'
import gururu from '@/assets/audio/gururu.mp3'
import 要坏掉了 from '@/assets/audio/要坏掉了.mp3'
import 转圈圈 from '@/assets/audio/转圈圈.mp3'
import 转圈圈咯 from '@/assets/audio/转圈圈咯.mp3'
import type {RunningItem} from "@/components/button/button";
import {reactive} from "vue";

// var props = defineProps<PropsOptions>()
const emits = defineEmits(['click'])
function click(){
    emits('click')
    addGif()
    play()
}
var runningList = reactive<Array<RunningItem>>([])
function addGif(){
    runningList.push({
        id: Date.now(), img: Math.random()>0.5?hertaa1:hertaa2
    })
    setTimeout(()=>{
        runningList.splice(0,1)
    },2000)
}
function play(){
    let audio = new Audio()
    audio.src=randomAudio()
    audio.play()
}
function randomAudio(){
    let arr = [gululu,gururu,要坏掉了,转圈圈,转圈圈咯]
    return arr[Math.floor(Math.random() * arr.length)]
}
</script>

<template>
    <div class="box" @click="click">
        <div class="gif">
            <img v-for="item in runningList" :src="item.img" :key="item.id" width="50" class="play">
        </div>
        <button class="btn"><slot name="default"/></button>
    </div>
</template>

<style scoped lang="scss">
.box{
    --font-color: rgb(243, 42, 98);
    --border-color: rgb(255, 203, 218);
    --hover-border-color: rgb(243, 155, 184);
    --focus-border-color: rgb(237, 11, 84);
    display: inline-block;
    .btn{
        padding: 10px 18px;
        background-color: white;
        border: 1px solid var(--border-color);
        color: var(--font-color);
        cursor: pointer;
        border-radius: 20px;
        transition: all .3s;
        &:hover{
            --color: var(--hover-color);
            --font-color: var(--hover-border-color);
        }
        &:active{
            --hover-color: var(--focus-border-color);
        }
    }
    .gif{
        width: 100%;
        position: relative;
        .play{
            animation-name: run;
            animation-duration: 2s;
            position: absolute;
            right: 0;
            top: -50px;
            opacity: 0;
        }
    }
}
@keyframes run {
    0%{
        opacity: 0;
        right: 0;
    }
    50%{
        opacity: 1;
    }
    100%{
        opacity: 0;
        right: calc(100% - 50px);
    }
}
</style>