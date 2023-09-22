<template src="./AppListTemplate.html"></template>

<script>
import AppHeader from "./AppHeader.vue";
// Import methods and data
import dataContent from './AppListData.json';

export default {
  name: "AppList",
  props: {
    msg: String
  },
  components: {
    AppHeader
  },
  computed: {
    isMobileDevice() {
      return /Android|webOS|iPhone|iPad|iPod|BlackBerry|Windows Phone/i.test(navigator.userAgent);
    }
  },

methods: {
    expandCard: function(event, index) {
      var el = event.currentTarget; 
      var body = document.body;
      if (
        !this.isMobileDevice
      ) {
        var distanceToTop = el.getBoundingClientRect().top;
        distanceToTop = -1 * distanceToTop;
        el.style.transform = "translateY(" + distanceToTop + "px)";
      } else {
        body.classList.toggle("mobile-scroll");
      }

      setTimeout(() => (this.transitionIndex = index), 200);

      this.transitioning = !this.transitioning;
      body.classList.toggle("no-scroll");
    }
  },
  data: function() {
    return dataContent;
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

<style scoped>
@import '../assets/AppListStyles.css';
</style>
