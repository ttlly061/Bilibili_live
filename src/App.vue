<template>
  <div id="app">
    <test msg ="test my first vue project"/>
  </div>
</template>

<script>
import test from "./components/test.vue"
export default {
  name: "App",
  components: {
    test,
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 50px 500px;
  width: 500px; 
  top: 0;
  right: 0;
  bottom: 0;
  border: 1px solid #21746100;
  border-radius: 12px;
  background: rgb(212, 212, 212);
}
</style>
