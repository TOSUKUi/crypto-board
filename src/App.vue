<template>
  <div id="app">
    <div class="md-layout">
      <div class="md-card">
        <div class="md-card-content">
          <Bitmex></Bitmex>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import HelloWorld from "./components/HelloWorld.vue";
import MyChart from "./components/MyChart.vue";
import Bitmex from "./components/Bitmex.vue";

export default {
  name: "app",
  components: {
    HelloWorld,
    MyChart,
    Bitmex
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
