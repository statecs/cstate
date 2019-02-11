<template>
  <div class="hello">
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
          <div class="Card-header-meta"></div>
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
              <span v-html="card.publish_date"></span>
              <span></span>
            </div>
          </div>
        </div>
        <div v-if="card.description" class="Card-body-description">
          <!-- <div style="overflow:scroll" v-html="card.description"></div>-->
          <div class="container-fluid content-holder">
            <div class="inner-content" data-position="20vh" data-position-expanded="40vh">
              <div class="info-holder">
                <div class="date-category" v-html="card.publish_date"></div>
                <div class="like-wrapper btn-liked">
                  <i class="fa fa-heart fa-lg"></i>
                  <span class="count"></span>
                </div>
                <div class="bookmark-wrapper btn-bookmark">
                  <i class="fa fa-bookmark-o fa-lg"></i>
                </div>
              </div>
              <h2 class="title" v-html="card.title"></h2>
              <div class="description" v-html="card.description"></div>
            </div>
          </div>
        </div>
      </a>
    </section>
  </div>
</template>

<script>
export default {
  name: "AppList",
  props: {
    msg: String
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
          message: "Project #1",
          publish_date: "July 2018",
          description:
            "This is the playful lorem ipsum of the ipsum lawlerH. This is the playful lorem ipsum of the ipsum lawlerH.  <br /><br /><br /><br /><br /> <img width='100%' src='https://images.unsplash.com/photo-1530435460869-d13625c69bbf?ixlib=rb-1.2.1&auto=format&fit=crop&w=1950&q=80'> This is the playful lorem ipsum of the ipsum lawlerH. <br> This is the playful lorem ipsum of the ipsum lawlerH. This is the playful lorem ipsum of the ipsum lawlerH. This is the playful lorem ipsum of the ipsum lawlerH. This is the playful lorem ipsum of the ipsum lawlerH. This is the playful lorem ipsum of the ipsum lawlerH. This is the playful lorem ipsum of the ipsum lawlerH. This is the playful lorem ipsum of the ipsum lawlerH. This is the playful lorem ipsum of the ipsum lawlerH. This is the playful lorem ipsum of the ipsum lawlerH.",
          cover:
            "https://images.unsplash.com/photo-1416339684178-3a239570f315?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1567&q=80",
          author: {
            name: "Malcom Fox",
            image:
              "https://images.unsplash.com/photo-1530435460869-d13625c69bbf?ixlib=rb-1.2.1&auto=format&fit=crop&w=1950&q=80"
          }
        },
        {
          message: "Project #2",
          publish_date: "July 2018",
          description:
            "This is the playful lorem ipsum of the ipsum lawlerH. This is the playful lorem ipsum of the ipsum lawlerH.  <br /><br /><br /><br /><br /> <img width='100%' src='https://images.unsplash.com/photo-1530435460869-d13625c69bbf?ixlib=rb-1.2.1&auto=format&fit=crop&w=1950&q=80'> This is the playful lorem ipsum of the ipsum lawlerH. <br> This is the playful lorem ipsum of the ipsum lawlerH. This is the playful lorem ipsum of the ipsum lawlerH. This is the playful lorem ipsum of the ipsum lawlerH. This is the playful lorem ipsum of the ipsum lawlerH. This is the playful lorem ipsum of the ipsum lawlerH. This is the playful lorem ipsum of the ipsum lawlerH. This is the playful lorem ipsum of the ipsum lawlerH. This is the playful lorem ipsum of the ipsum lawlerH. This is the playful lorem ipsum of the ipsum lawlerH.",
          cover:
            "https://images.unsplash.com/photo-1517694712202-14dd9538aa97?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1950&q=80",
          author: {
            name: "Malcom Fox",
            image:
              "https://pbs.twimg.com/profile_images/565258371092070400/kbW-3WU0.jpeg"
          }
        },
        {
          message: "Project #3",
          publish_date: "July 2018",
          cover:
            "https://images.unsplash.com/photo-1532510987384-6a8118ab6ab2?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1608&q=80",
          author: {
            name: "Malcom Fox",
            image:
              "https://pbs.twimg.com/profile_images/565258371092070400/kbW-3WU0.jpeg"
          }
        },
        {
          message: "Project #4",
          publish_date: "July 2018",
          cover:
            "https://images.unsplash.com/photo-1528879342222-323df0d65c9f?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=crop&w=1951&q=80",
          author: {
            name: "Malcom Fox",
            image:
              "https://pbs.twimg.com/profile_images/565258371092070400/kbW-3WU0.jpeg"
          }
        },
        {
          message: "Project #5",
          publish_date: "July 2018",
          cover:
            "https://images.unsplash.com/photo-1535598745644-bc7913bb1a2a?ixlib=rb-1.2.1&auto=format&fit=crop&w=1955&q=80",
          author: {
            name: "Malcom Fox",
            image:
              "https://pbs.twimg.com/profile_images/565258371092070400/kbW-3WU0.jpeg"
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
  overflow: auto;
  right: 0;
  top: 0;
  z-index: 9999;
  min-height: 100vh;
}
body.mobile-scroll.no-scroll div#app div.hello section a.Card.is-active {
  height: 100vh;
  position: fixed;
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

.Card.is-active:after {
  height: 100vh;
}
.Card:active {
  -webkit-transform: scale(0.95);
  transform: scale(0.95);
}
.Card-header {
  display: flex;
  width: 100%;
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
.content-holder {
  margin: 0 auto;
  padding: 0;
  z-index: 1;
  height: 100%;
  background-color: transparent;
  position: relative;
}

.inner-content {
  margin: 0 auto;
  max-width: 60vw;
  top: 10vh;
  padding: 50px;
  position: relative;
  background-color: #fff;
}

.inner-content {
  padding-bottom: env(safe-area-inset-bottom); /* for iPhone X */
  border-top-left-radius: 20px;
  border-top-right-radius: 20px;
}
</style>
