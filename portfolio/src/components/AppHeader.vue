<template>
  <header v-on:click.stop class="AppHeader" v-bind:class="{ 'is-removed' : transitioning }">
    <!-- <div :class="['container', { 'change': toggled }]" @click="myFunction">
      <div class="bar1"></div>
      <div class="bar2"></div>
      <div class="bar3"></div>
    </div>-->
    <!-- <div class="sticky-wrapper">
      <nav class="subnav">
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
    </div>-->
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
      transitionFixedIndex: null
    };
  },
  methods: {
    myFunction() {
      this.toggled = !this.toggled;
    }
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
  padding: 3rem 0;
  background-color: #fff;
}
.subnav.stuck {
  animation: b 0.2s ease forwards;
  background-color: #fff;
  border-bottom: none;
  left: 0;
  position: fixed;
  top: 0;
  width: 100%;
  z-index: 1000;
  padding-top: 0;
  padding-bottom: 2rem;
}

.row {
  max-width: 1300px;
  margin-right: auto;
  margin-left: auto;
}
</style>
