<template>
  <div class="block" @click="stopTimer" v-if="showblock">Click</div>
</template>

<script>
export default {
    props:['delay'],
    data() {
        return {
            showblock: false,
            timer: null,
            reactionTime: 0
        }
    },
    mounted() {
        setTimeout(() => {
            this.showblock = true
            this.startTimer()
        },this.delay)
    },
    methods: {
        startTimer() {
            this.timer = setInterval(() => {this.reactionTime += 10}, 10)
        },
        stopTimer() {
            clearInterval(this.timer)
            this.$emit('end', this.reactionTime)
        } 
        
    }
}
</script>


<style>
.block {
    position: absolute;
    width: 75px;
    height: 75px;
    border-radius: 50%;
    background-color: #40b882;
    color: #35495e;
    font-size: 15px;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
}
</style>