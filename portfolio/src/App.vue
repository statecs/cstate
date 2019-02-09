<template>
  <div id="app">
    <AppHeader></AppHeader>
    <AppList msg="Welcome to Your Vue.js App"/>
  </div>
</template>

<script>
import AppHeader from "./components/AppHeader.vue";
import AppList from "./components/AppList.vue";

export default {
  name: "app",
  components: {
    AppHeader,
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
</style>
