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
          <div class="container-fluid content-holder">
            <div
              v-bind:id="'scroll-'+card.id"
              v-on:click.stop
              class="inner-content"
              data-position="20vh"
              data-position-expanded="40vh"
            >
              <AppHeader v-if="transitionIndex !== null && transitioning"/>

              <div class="container-content">
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

                <div class="left-first-img container">
                  <img :src="card.cover">
                  <h1 v-html="card.message">Studs</h1>
                </div>
                <div class="details">
                  <div class="list">
                    <p>
                      Year:
                      <span v-html="card.year"></span>
                    </p>
                    <p>
                      Tech:
                      <span v-html="card.tech"></span>
                    </p>
                    <p>
                      Role:
                      <span v-html="card.title"></span>
                    </p>
                    <a v-if="card.url" target="_blank" :href="card.url">Go to project</a>
                  </div>
                </div>

                <div class="main-description">
                  <p v-html="card.description"></p>
                </div>
                <div v-for="item in card.content">
                  <div v-if="item.id === 'overview'" class="right-img">
                    <img :src="item.img">
                    <p v-html="item.caption"></p>
                  </div>

                  <div v-if="item.id === 'field-research'" class="left-img">
                    <img :src="item.img">
                    <p v-html="item.caption"></p>
                  </div>

                  <div v-if="item.id === 'prototyping'" class="right-img">
                    <img :src="item.img">
                    <p v-html="item.caption"></p>
                  </div>

                  <div v-if="item.id === 'visual'" class="left-img">
                    <img :src="item.img">
                    <p v-html="item.caption"></p>
                  </div>

                  <div v-if="item.id === 'other'">
                    <div v-html="item.html"></div>
                    <p v-html="item.caption"></p>
                  </div>
                  <div v-if="item.id === 'other'" class="right-img">
                    <img :src="item.img">
                  </div>

                  <!--<div :id="item.id" v-html="item.content"></div>-->
                </div>
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
          subtitle: "Sketch, InDesign | July 2018",
          tech: "Sketch/ InDesign",
          year: "July 2018",
          url: "https://studieresan.se",
          description:
            "Studs, or the Study Trip, is an annual project at the Department of Computer Science at the Royal Institute of Technology (KTH) in Stockholm. The project aims to create a platform for interaction between students close to graduation and relevant companies. The project ends with a study trip to give the students an opportunity to meet companies abroad. The report itself serves as the major delivery in the course, serving as a record of the project.",
          content: [
            {
              id: "overview",
              img: "http://cstate.se/assets/studs_cygni.jpg",
              caption: "Screenshot of the layout of the report."
            },
            {
              id: "field-research",
              img: "http://cstate.se/assets/studs_kry.jpg",
              caption: "Screenshot of the layout of the report."
            },
            {
              id: "other",
              html:
                "<iframe width='100%' height='800px' frameBorder='0' src='https://drive.google.com/file/d/1X8-gNNXPlpWrLF4Uf1I9xj2caoDKi7ws/view?usp=sharing'> ",
              caption: "Report"
            }
          ],
          cover: "http://cstate.se/assets/studs_screen7.jpg",
          author: {
            name: "Studs",
            image: ""
          }
        },
        {
          id: "2",
          message: "THS Website",
          title: "UX Developer",
          subtitle: "AngularJS | 2017-2018",
          tech: "Angular/ CSS/ HTML",
          year: "2017-2019",
          url: "https://ths.kth.se",
          description:
            "Responsive Angular 4 Web Application designed to work with the WordPress JSON REST API.",
          content: [
            {
              id: "overview",
              img: "http://cstate.se/assets/intro_ths.jpg",
              caption: ""
            },
            {
              id: "field-research",
              img: "http://cstate.se/assets/powerpoint_ths.jpg",
              caption: ""
            },
            {
              id: "prototyping",
              img: "http://cstate.se/assets/ths_desktop_1.jpg",
              caption: ""
            },
            {
              id: "visual",
              img: "",
              caption: ""
            },
            {
              id: "other",
              html: ""
            }
          ],
          cover: "http://cstate.se/assets/ths_screen1.jpg",
          author: {
            name: "THS",
            image: ""
          }
        },
        {
          id: "3",
          message: "CreativeStudio",
          title: "UX Developer",
          subtitle: "HTML5/ PHP/ Javascript | August 2018",
          tech: "Angular/ CSS/ HTML",
          year: "August 2018",
          url: "https://creativestudio.nu",
          description:
            "Graphical identity and website developed in Wordpress. ",
          content: [
            {
              id: "overview",
              img: "http://cstate.se/assets/creativestudio_screen6.jpg",
              caption: ""
            },
            {
              id: "field-research",
              img: "http://cstate.se/assets/creativestudio_screen4.jpg",
              caption: ""
            },
            {
              id: "prototyping",
              img: "http://cstate.se/assets/creativestudio_screen3.jpg",
              caption: ""
            },
            {
              id: "visual",
              img: "http://cstate.se/assets/creativestudio_screen2.jpg",
              caption: ""
            }
          ],
          cover: "http://cstate.se/assets/creativestudio_screen8.jpg",
          author: {
            name: "Creativestudio",
            image: ""
          }
        },
        {
          id: "4",
          message: "Gameful self-directed learning",
          title: "Designer",
          subtitle: "inVision Studio | December 2018",
          tech: "UI/ UX",
          year: "December 2018",
          url: "",
          description:
            "This project was developed as part of a collaboration between KTH and Kanda University of International Studies (KUIS) in Japan. The interactive prototype has been created in inVision Studio, using gameful elements categorized into three categories, i.e., objective, progression and feedback. Objective - A behavioral mechanic type, requiring the user to take action for the reward, Progression - Move the user through the content. Feedback - Informing the user of their status.",
          content: [
            {
              id: "overview",
              img: "http://cstate.se/assets/gameful_first_1.jpg",
              caption: "Moodboard of the first ideation phase"
            },
            {
              id: "field-research",
              img: "http://cstate.se/assets/gameful_second.jpg",
              caption:
                "A prototype for a gameful self-directed learning application developed for Japanese students"
            },
            {
              id: "prototyping",
              img: "http://cstate.se/assets/powerpoint_ths.jpg",
              caption:
                "A prototype for a gameful self-directed learning application developed for Japanese students"
            },
            {
              id: "visual",
              img: "http://cstate.se/assets/ths_desktop_1.jpg",
              caption:
                "A prototype for a gameful self-directed learning application developed for Japanese students"
            },
            {
              id: "other",
              html:
                "<iframe width='100%' height='315' frameBorder='0' src='https://www.youtube.com/embed/PIDCoaKP2hM' frameborder='0' allow='accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture' allowfullscreen></iframe>"
            }
          ],
          cover: "http://cstate.se/assets/gameful_screen13.jpg",
          author: {
            name: "KTH",
            image: ""
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
  padding: 15px;
  position: relative;
  min-height: 460px;
  background-size: cover;
  max-width: 100vw;
  margin: 20px auto;
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
  max-width: 100vw;
  margin: 0px auto;
  -webkit-overflow-scrolling: touch;
  bottom: 0;
  left: 0;
  right: 0;
  top: 0;
  padding: 0;
  z-index: 9999;
  min-height: 100vh;
  border-radius: 0px;
  background-image: none !important;
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
  color: white;
  text-align: left;
  line-height: 1.7em;
}

/* .Card:active {
  -webkit-transform: scale(0.95);
  transform: scale(0.95);
}*/
.Card-header {
  display: flex;
  width: 100%;
}
.Card.is-active .Card-header {
  padding: 15px;
  justify-content: flex-end;
  margin-left: -30px;
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
  padding: 0;
  z-index: 1;
  background-color: transparent;
  position: relative;
}

.container-content {
  margin: 0 auto;
}

.inner-content {
  height: 100vh;
  overflow: scroll;
  margin: 0 auto;
  max-width: 100vw;
  top: 0;
  padding: 15px;
  position: relative;
  overflow: scroll;
  z-index: 1;
  background-color: transparent;
  position: relative;
}

.inner-content {
  padding-bottom: env(safe-area-inset-bottom); /* for iPhone X */
  border-top-left-radius: 20px;
  border-top-right-radius: 20px;
}

.details {
  font-size: 13px;
}

.details .list p {
  padding: 0;
  margin: 0;
}

.left-img {
  text-align: left;
}
.left-first-img {
  max-width: 103%;
  overflow-x: hidden;
  overflow: hidden;
}
.left-first-img h1 {
  margin-left: 15%;
  margin-top: -40px;
  padding-right: 400px;
  font-size: 100px;
  color: #f3f3f3;
  margin-bottom: 80px;
  width: 1000%;
}
.container {
  width: 100vw;
}
.left-first-img img {
  max-height: 400px;
  width: 95%;
  object-fit: cover;
}
.left-img img {
  max-width: 100%;
}
.right-img {
  text-align: right;
  padding-top: 50px;
  padding-bottom: 70px;
}
.right-img img {
  max-width: 100%;
}
.main-description {
  margin-top: 30px;
}

@media screen and (min-width: 480px) {
  .left-first-img {
    max-width: 106%;
  }
  .left-first-img h1 {
    margin-left: 10%;
    margin-top: -50px;
    font-size: 150px;
  }
  .inner-content {
    padding: 0 50px;
  }
}
@media screen and (min-width: 769px) {
  .Card.is-active .Card-header {
    padding: 15px;
    justify-content: space-between;
    margin-left: 0;
  }

  .right-img {
    text-align: right;
    padding-top: 150px;
    padding-bottom: 80px;
  }
  .left-img img {
    max-width: 700px;
  }
  .right-img img {
    max-width: 700px;
  }
  .Card-body-title {
    text-align: center;
    font-size: 1.3em;
  }
  .left-first-img h1 {
    font-size: 250px;
    margin-bottom: 150px;
  }
  .Card.is-active .Card-header {
    padding: 30px;
  }
  .main-description {
    float: right;
    max-width: 50%;
    margin-top: -100px;
  }
}
@media screen and (min-width: 1024px) {
  .container-content {
    max-width: 70vw;
    padding: 50px 100px;
  }
  .left-first-img img {
    max-height: 800px;
  }
  .left-first-img h1 {
    margin-bottom: 170px;
  }
  .Card.is-active .Card-header-add {
    width: 48px;
    height: 48px;
  }
  .Card.is-active .PlusIcon:before,
  .Card.is-active .PlusIcon:after {
    height: 20px;
    margin: 7px 0px;
  }
}
@media only screen and (min-width: 1440px) {
  .Card {
    max-width: 70vw;
    /* styles here */
  }
  .container-content {
    max-width: 60vw;
    padding: 50px 100px;
  }
}
@media only screen and (min-width: 1680px) {
  .right-img img {
    max-width: 900px;
  }
  .left-img img {
    max-width: 900px;
  }
}
@media only screen and (min-width: 1920px) {
  .Card {
    max-width: 65vw;
    /* styles here */
  }
  .container-content {
    max-width: 50vw;
  }
}
</style>
