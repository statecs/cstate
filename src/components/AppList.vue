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

    // Logging for debugging
    console.log("Device:", this.isMobileDevice ? "Mobile" : "Non-Mobile");
    
    if (!this.isMobileDevice) {

      if (el.style.transform && el.style.transform !== "translateY(0px)") {
        // If there's a transform applied, and it's not the default, reset it.
        el.style.transform = "translateY(0px)";
      } else {
        var distanceToTop = el.getBoundingClientRect().top;
        console.log("Initial distanceToTop:", distanceToTop);  // Log initial value

        if (distanceToTop < 0) {
          // If the element is already above the viewport, reset the transform
          //el.style.transform = "translateY(0px)";
          el.style.transform = "translateY(" + -distanceToTop + "px)";
          console.log("Element above viewport. Resetting transform.");
        } else {
          distanceToTop = -1 * distanceToTop;
          console.log("Adjusted distanceToTop:", distanceToTop);  // Log adjusted value

          // Fix: Ensure distanceToTop is set to 0 if it's an unexpected value.
          if (Math.abs(distanceToTop) > window.innerHeight) {
            distanceToTop = 0;
            console.warn("Unexpected distanceToTop value. Resetting to 0.");
          }

          el.style.transform = "translateY(" + distanceToTop + "px)";
        }
      }
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
