<template>
  <header v-on:click.stop class="AppHeader" v-bind:class="{ 'is-removed' : transitioning }">
    <!-- <div :class="['container', { 'change': toggled }]" @click="myFunction">
      <div class="bar1"></div>
      <div class="bar2"></div>
      <div class="bar3"></div>
    </div>-->
    <div class="sticky-wrapper" :style="[scrollPosition > 100 ? {'height':'60px'}: {} ]">
      <nav class="subnav" :class="{stuck: scrollPosition > 100}">
        <div class="row">
          <ul>
            <li>
              <a href="#overview" class="anchor_link">Overview</a>
            </li>
            <li>
              <a href="#field-research" class="anchor_link active">Field Research</a>
            </li>
            <li>
              <a href="#engagement-strategy" class="anchor_link">Prototyping</a>
            </li>
            <li>
              <a href="#visual-program" class="anchor_link">Visual Design</a>
            </li>
          </ul>
        </div>
      </nav>
    </div>
  </header>
</template>

<script>
export default {
  name: "AppHeader",
  props: {
    msg: String
  },
  data: function() {
    return {
      toggled: false,
      title: "Featured Projects",
      transitioning: false,
      transitionIndex: null,
      transitionFixedIndex: null,
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
    },
    updateScroll4() {
      this.scrollPosition = document.getElementById("scroll-4").scrollTop;
    },
    myFunction() {
      this.toggled = !this.toggled;
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
    document
      .getElementById("scroll-4")
      .addEventListener("scroll", this.updateScroll4);
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.bar1,
.bar2,
.bar3 {
  width: 35px;
  height: 5px;
  background-color: #333;
  margin: 6px 0;
  transition: 0.4s;
}

.change .bar1 {
  -webkit-transform: rotate(-45deg) translate(-9px, 6px);
  transform: rotate(-45deg) translate(-9px, 6px);
}

.change .bar2 {
  opacity: 0;
}

.change .bar3 {
  -webkit-transform: rotate(45deg) translate(-8px, -8px);
  transform: rotate(45deg) translate(-8px, -8px);
}
.subnav {
  border-bottom: 1px solid #dbdbdb;
  background-color: #fff;
}
.subnav.stuck {
  animation: b 0.2s ease forwards;
  background-color: #fff;
  border-bottom: none;
  position: fixed;
  top: 0;
  width: 88vw;
  z-index: 1000;
  padding-top: 0;
  padding-bottom: 2rem;
  text-align: center;
  height: 25px;
}

.row {
  max-width: 1300px;
  margin-right: auto;
  margin-left: auto;
}
</style>
