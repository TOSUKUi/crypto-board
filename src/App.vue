<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <div class="md-layout">
      <div class="md-card">
        <div class="md-card-content">
            <MyChart :width="640" :height="480"></MyChart>
        </div>
      </div>
      <div class="md-card">
        <div class="md-card-content">
          <Bitmex></Bitmex>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import MyChart from './components/MyChart.vue'
import BitmexOI from './components/BitmexOI.vue'
import Bitmex from './components/Bitmex.vue'

export default {
  name: 'app',
  components: {
    HelloWorld,
    MyChart,
    BitmexOI,
    Bitmex
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
