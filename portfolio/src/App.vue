<template>
  <div id="app">
    <AppList msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import AppList from "./components/AppList.vue";

export default {
  name: "app",
  components: {
    AppList
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
body.no-scroll {
  overflow: hidden;
}
</style>
