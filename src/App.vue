<template>
  <div class="main">

    <div class="top">
      <img alt="Vue logo" src="./assets/logo.png">
      <h1>Vue Reaction Timer</h1>
      <result v-if="showresult" :score="score"></result>
      <button @click="start" :disabled="isplaying">Play</button>
    </div>

    <div ref="container" class="bottom">
      <block :style="position" ref="box" v-if="isplaying" :delay="delay" @end="endgame"></block>
    </div>  
  </div>
</template>

<script>

import block from './components/block.vue'
import result from './components/result.vue'

export default {
  name: 'App',
  components: { block, result },
  data() {
    return {
      isplaying: false,
      delay: null,
      score: null,
      showresult: false,
      position: {}
    }
  },
  methods: {
    start() {
      this.isplaying = true
      this.delay = 2000 + Math.random() * 5000
      this.showresult = false

      /* Box random spawn */

      const container = this.$refs.container
      const containerwidth = container.clientWidth
      const containerheight = container.clientHeight

      const boxwidth = 50
      const boxheight = 50

      const x = Math.floor(Math.random() * (containerwidth - boxwidth))
      const y = Math.floor(Math.random() * (containerheight - boxheight))
      
      this.position = {left: `${x}px`, top: `${y}px`}
    },
    endgame(reactionTime) {
      this.score = reactionTime
      this.isplaying = false
      this.showresult = true
    }
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #35495e;
}
.main {
  height: 100vh;
  width: 100%;
  padding: 0 5%;
}
.top {
  width: 100%;
  height: 50%;
  display: flex;
  flex-direction: column;
  justify-content: space-evenly;
  align-items: center;
}
.top img {
  width: 100px;
  height: 100px;
}
.top h1 {
  font-weight: 900;
}
.top button {
  padding: 10px 50px;
  color: #40b882;
  font-weight: bold;
  font-size: 15px;
  border: 1px solid #40b882;
  background-color: #35495e;
  cursor: pointer;
}
.top button:hover {
  color: #35495e;
  background-color: #40b882;
}
.top button[disabled] {
  opacity: 0.5;
  cursor: not-allowed;
}
.top button[disabled]:hover {
  color: #40b882;
  border: 1px solid #40b882;
  background-color: #35495e;
}
.bottom {
  position: relative;
  width: 100%;
  height: 50%;
  overflow: hidden;
}
@media (min-width: 992px){
  .bottom {
    width: 50%;
    height: 50%;
    margin: 0 auto;
    border: 2.5px #35495e;
    border-style: solid solid none solid;
  }
}
</style>
