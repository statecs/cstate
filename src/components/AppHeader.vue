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
  mounted: function() {
    document
      .getElementById("scroll-1")
      .addEventListener("scroll", this.updateScroll1);
    document
      .getElementById("scroll-2")
      .addEventListener("scroll", this.updateScroll2);
    document
      .getElementById("scroll-3")
      .addEventListener("scroll", this.updateScroll3);
  }
};
</script>
