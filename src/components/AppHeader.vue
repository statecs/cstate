<template>
  <header v-on:click.stop class="AppHeader" v-bind:class="{ 'is-removed' : transitioning }">
  </header>
</template>

<script>
export default {
  name: "AppHeader",
  data: function() {
    return {
      transitioning: false,
      scrollPosition: null
    };
  },
  methods: {
    updateScroll1() {
      this.scrollPosition = document.getElementById("scroll-1").scrollTop;
    },
    updateScroll2() {
      this.scrollPosition = document.getElementById("scroll-2").scrollTop;
    },
    updateScroll3() {
      this.scrollPosition = document.getElementById("scroll-3").scrollTop;
    }
  },
};
</script>
