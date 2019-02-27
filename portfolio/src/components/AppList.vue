<template>
  <div class="hello">
    <!-- <h1>Yolo</h1>
    <h2>I hope you are good!</h2>My name is Christopher State. I am currently studying Interactive Media Technology at KTH. My passion is to create solutions with the user in mind. I have interests in fields from development, design to communcations and marketing. Recently I am very fond of conversational interfaces and how one can use empathy. In my freetime I like to meditate, bike and read.
    <br>
    <br>LinkedIn, Twitter, E-Mail, Pidgeon (Postal)-->
    <section>
      <a
        href="#"
        class="Card"
        v-for="(card,index) in items"
        :key="index.id"
        v-bind:style="{ 'background-image': 'url(' + card.cover + ')' }"
        v-on:click.prevent="transitionToFull($event, index)"
        v-bind:class="{
                      'is-active': transitionIndex === index && transitioning
                     }"
      >
        <header class="Card-header">
          <div class="Card-header-add">
            <button type="button">
              <button type="button" class="PlusIcon"></button>
            </button>
          </div>
        </header>
        <div class="Card-body">
          <div class="Card-body-title">
            <h2>{{ card.message }}</h2>
            <p v-if="card.description" class="Card-body-description">
              <!-- {{ card.description }}-->
            </p>
            <div>
              <span v-html="card.title"></span>
              <br>
              <span v-html="card.subtitle"></span>
            </div>
          </div>
        </div>
        <div v-if="card.description" class="Card-body-description">
          <!-- <div style="overflow:scroll" v-html="card.description"></div>-->
          <div v-bind:id="'scroll-'+card.id" class="container-fluid content-holder">
            <div
              v-on:click.stop
              class="inner-content"
              data-position="20vh"
              data-position-expanded="40vh"
            >
              <AppHeader v-if="transitionIndex !== null && transitioning"/>
              <div class="info-holder">
                <div class="like-wrapper btn-liked">
                  <i class="fa fa-heart fa-lg"></i>
                  <span class="count"></span>
                </div>
                <div class="bookmark-wrapper btn-bookmark">
                  <i class="fa fa-bookmark-o fa-lg"></i>
                </div>
              </div>
              <!--<h2 class="title" v-html="card.title"></h2>
              <h2 class="title" v-html="card.subtitle"></h2>-->
              <div v-for="item in card.description" :key="item">
                <div v-html="item"></div>
              </div>
            </div>
          </div>
        </div>
      </a>
    </section>
  </div>
</template>

<script>
import AppHeader from "./AppHeader.vue";

export default {
  name: "AppList",
  props: {
    msg: String
  },
  components: {
    AppHeader
  },
  methods: {
    transitionToFull: function(event, index) {
      var el = event.currentTarget; //target;
      var body = document.body;
      //var distanceToTop = Math.abs(el.getBoundingClientRect().top);
      //console.log(distanceToTop);
      if (
        !(
          navigator.userAgent.match(/Android/i) ||
          navigator.userAgent.match(/webOS/i) ||
          navigator.userAgent.match(/iPhone/i) ||
          navigator.userAgent.match(/iPad/i) ||
          navigator.userAgent.match(/iPod/i) ||
          navigator.userAgent.match(/BlackBerry/i) ||
          navigator.userAgent.match(/Windows Phone/i)
        )
      ) {
        var distanceToTop = el.getBoundingClientRect().top;
        distanceToTop = -1 * distanceToTop;
        el.style.transform = "translateY(" + distanceToTop + "px)";
      } else {
        body.classList.toggle("mobile-scroll");
      }

      setTimeout(() => (this.transitionIndex = index), 200);

      //  if (navigator.userAgent.match(/(iPhone|iPod|iPad)/i)) {
      //  var scrollPos = 0;
      //scrollPos = window.scrollTo(0, 0).offset().top;
      //}

      //$(window).scrollTop(scrollPos);
      // window.scrollTo(0, 0);

      //console.log(distanceToTop);
      this.transitioning = !this.transitioning;
      body.classList.toggle("no-scroll");
      //body.style.overflow = "hidden";
    }
  },
  data: function() {
    return {
      toggled: false,
      title: "Featured Articles",
      transitioning: false,
      transitionIndex: null,
      transitionFixedIndex: null,
      items: [
        {
          id: "1",
          message: "Studs - Studieresan",
          title: "Art Director",
          subtitle: "Sketch, InDesign | Summer 2018",
          description: [
            "<img width='100%' src='http://cstate.se/assets/studs_screen4.jpg'>",
            "<img width='100%' src='http://cstate.se/assets/studs_screen2.jpg'>",
            "<img width='100%' src='http://cstate.se/assets/studs_screen5.jpg'>",
            "<iframe width='100%' height='800px' src='https://drive.google.com/file/d/1X8-gNNXPlpWrLF4Uf1I9xj2caoDKi7ws/view?usp=sharing'>"
          ],
          cover: "http://cstate.se/assets/studs_screen1.jpg",
          author: {
            name: "Creativestudio",
            image:
              "https://images.unsplash.com/photo-1530435460869-d13625c69bbf?ixlib=rb-1.2.1&auto=format&fit=crop&w=1950&q=80"
          }
        },
        {
          id: "2",
          message: "Key-experience",
          title: "ME2818 Design Thinking",
          subtitle: "Sketch | February 2019",
          description: [
            "<img src='http://cstate.se/assets/Cardinal_screen1.png'>",
            "<img src='http://cstate.se/assets/Cardinal_screen2.png'>",
            "<img src='http://cstate.se/assets/Cardinal_screen3.png'>",
            "<img src='http://cstate.se/assets/Cardinal_screen4.png'>"
          ],
          cover: "http://cstate.se/assets/Cardinal_screen5.jpeg",
          author: {
            name: "Creativestudio",
            image:
              "https://images.unsplash.com/photo-1530435460869-d13625c69bbf?ixlib=rb-1.2.1&auto=format&fit=crop&w=1950&q=80"
          }
        },
        {
          id: "3",
          message: "THS Website",
          title: "UX Developer",
          subtitle: "AngularJS | 2017/2019",
          description: [
            "<a href='https://kths.se/'>Link to website</a>",
            "<img width='100%' src='http://cstate.se/assets/ths_screen6.png'>"
          ],
          cover: "http://cstate.se/assets/ths_screen1.jpg",
          author: {
            name: "Malcom Fox",
            image:
              "https://pbs.twimg.com/profile_images/565258371092070400/kbW-3WU0.jpeg"
          }
        },
        {
          id: "4",
          message: "CreativeStudio",
          title: "UX Developer",
          subtitle: "HTML5/PHP/Javascript | Summer 2018",
          description: [
            "<img width='100%' src='http://cstate.se/assets/creativestudio_screen6.jpg'>",
            "<img width='100%' src='http://cstate.se/assets/creativestudio_screen4.jpg'>",
            "<img width='100%' src='http://cstate.se/assets/creativestudio_screen3.jpg'>",
            "<img width='100%' src='http://cstate.se/assets/creativestudio_screen2.jpg'>"
          ],
          cover: "http://cstate.se/assets/creativestudio_screen8.jpg",
          author: {
            name: "Creativestudio",
            image:
              "https://images.unsplash.com/photo-1530435460869-d13625c69bbf?ixlib=rb-1.2.1&auto=format&fit=crop&w=1950&q=80"
          }
        }
      ]
    };
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.AppList {
  margin: 0 auto;
}

.no-scroll .app-popup-window {
  position: fixed;
  z-index: 1;
}

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
button {
  padding: 0;
  background: none;
  border: none;
}
button:focus {
  outline: none;
}

.PlusIcon {
  position: relative;
  width: 100%;
  height: 100%;
}
.PlusIcon:before,
.PlusIcon:after {
  content: "";
  display: block;
  width: 2px;
  height: 16px;
  background-color: currentColor;
  position: absolute;
  top: 50%;
  left: 50%;
  -webkit-transform: translate(-50%, -50%);
  transform: translate(-50%, -50%);
}
.PlusIcon:after {
  -webkit-transform: translate(-50%, -50%) rotate(90deg);
  transform: translate(-50%, -50%) rotate(90deg);
}
.Card {
  box-shadow: 0 23px 7px -21px rgba(0, 0, 0, 0.5);
  background-color: black;
  background-position: center center;
  color: white;
  border-radius: 15px;
  display: flex;
  flex-direction: column;
  margin: 20px;
  padding: 15px;
  position: relative;
  min-height: 460px;
  background-size: cover;
  text-decoration: none;
  transition: margin-left 120ms ease, margin-right 120ms ease,
    margin-top 120ms ease, border-radius 120ms ease, left 520ms ease,
    right 520ms ease, top 520ms ease, height 520ms ease,
    -webkit-transform 320ms ease 250ms;
  transition: transform 320ms ease 250ms, margin-left 120ms ease,
    margin-right 120ms ease, margin-top 120ms ease, border-radius 120ms ease,
    left 520ms ease, right 520ms ease, top 520ms ease, height 520ms ease;
  transition: transform 320ms ease 250ms, margin-left 120ms ease,
    margin-right 120ms ease, margin-top 120ms ease, border-radius 120ms ease,
    left 520ms ease, right 520ms ease, top 520ms ease, height 520ms ease,
    -webkit-transform 320ms ease 250ms;
}
.Card:after {
  background-color: #fff;
  content: "";
  display: block;
  position: absolute;
  top: 100%;
  left: 0;
  right: 0;
  height: 0;
  transition: height 400ms ease-out 200ms;
  z-index: -1;
}

.Card.is-active {
  margin: 0px;
  -webkit-overflow-scrolling: touch;
  bottom: 0;
  left: 0;
  right: 0;
  top: 0;
  padding: 0;
  z-index: 9999;
  min-height: 100vh;
}
body.mobile-scroll.no-scroll div#app div.hello section a.Card.is-active {
  height: 100vh;
  position: fixed;
}
a.Card .Card-body-description {
  overflow: hidden;
}
a.Card.is-active .Card-body-description {
  overflow: visible;
}

.Card.is-active .Card-header-add {
  -webkit-transform: rotate(135deg);
  transform: rotate(135deg);
}
.Card.is-active .Card-body-description {
  opacity: 1;
  -webkit-transform: scale(1);
  transform: scale(1);
  padding-top: 0;
  z-index: 999;
  color: black;
  text-align: left;
  line-height: 1.7em;
}

.Card:active {
  -webkit-transform: scale(0.95);
  transform: scale(0.95);
}
.Card-header {
  display: flex;
  width: 100%;
}
.Card.is-active .Card-header {
  position: fixed;
  padding: 15px;
}
.Card-header-add {
  background-color: #fff;
  border-radius: 100%;
  width: 32px;
  height: 32px;
  transition: -webkit-transform 200ms ease 500ms;
  transition: transform 200ms ease 500ms;
  transition: transform 200ms ease 500ms, -webkit-transform 200ms ease 500ms;
}
.Card-body-title {
  text-align: center;
}
@media screen and (min-width: 768px) {
  .Card-body-title {
    text-align: center;
    font-size: 1.3em;
  }
  a.Card.is-active .Card-body-description {
    padding: 0 60px;
  }
}
.Card-body-description {
  opacity: 0;
  height: 0;
  -webkit-transform: translate(0, 5px) scale(0.85);
  transform: translate(0, 5px) scale(0.85);
  transition: opacity 200ms ease 200ms, height 200ms ease 200ms,
    -webkit-transform 200ms ease 200ms;
  transition: transform 200ms ease 200ms, opacity 200ms ease 200ms,
    height 200ms ease 200ms;
  transition: transform 200ms ease 200ms, opacity 200ms ease 200ms,
    height 200ms ease 200ms, -webkit-transform 200ms ease 200ms;
}

/** **/
.Card.is-active .Card-body {
  display: none;
}
.content-holder {
  margin: 0 auto;
  padding: 60px 0;
  z-index: 1;
  height: 100vh;
  overflow: scroll;
  background-color: transparent;
  position: relative;
}

.inner-content {
  margin: 0 auto;
  max-width: 100vw;
  top: 0;
  padding: 50px;
  position: relative;
  overflow: scroll;
  background-color: #fff;
}
body.mobile-scroll.no-scroll
  div#app
  section
  a.Card.is-active
  div.Card-body-description
  div.container-fluid.content-holder
  div.inner-content {
  padding: 50px 20px;
}
body.mobile-scroll.no-scroll
  div#app
  section
  a.Card.is-active
  div.Card-body-description
  div.container-fluid.content-holder
  div.inner-content
  div
  div
  img {
  width: 300px;
  max-width: 100%;
}
.inner-content {
  padding-bottom: env(safe-area-inset-bottom); /* for iPhone X */
  border-top-left-radius: 20px;
  border-top-right-radius: 20px;
}
.inner-content div div img {
  max-width: 300px;
}
</style>
