<template>
  <div class="hello">
    <nav>
      <a href="#" v-if="showProjects" v-on:click="showProjects = false">
        <p>
          <svg
            class="back"
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 24 24"
            fill="black"
            width="18px"
            height="18px"
          >
            <path d="M0 0h24v24H0z" fill="none" />
            <path d="M21 11H6.83l3.58-3.59L9 6l-6 6 6 6 1.41-1.41L6.83 13H21z" />
          </svg>About me
        </p>
      </a>
      <a href="#projects" v-else v-on:click="showProjects = true">
        <p>
          All projects
          <svg
            xmlns="http://www.w3.org/2000/svg"
            viewBox="0 0 24 24"
            fill="black"
            width="18px"
            height="18px"
          >
            <path d="M0 0h24v24H0z" fill="none" />
            <path d="M16.01 11H4v2h12.01v3L20 12l-3.99-4z" />
          </svg>
        </p>
      </a>
    </nav>

    <section v-if="showProjects">
      <a
        href="#"
        class="Card"
        v-for="(card,index) in items"
        v-if="index >= 1"
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
              <br />
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
              <AppHeader v-if="transitionIndex !== null && transitioning" />

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
                  <img :src="card.cover" alt="Image">
                  <h1 v-html="card.heading"></h1>
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
                    <a v-if="card.url" target="_blank" :href="card.url" aria-label="Opens the project a new tab">Go to project</a>
                    <p>
                      <a v-if="card.figma" target="_blank" :href="card.figma" aria-label="Opens Figma a new tab">
                        <img class="git-logo" src="https://cstate.se/assets/figma-logo.png" alt="Image">
                      </a>
                      <a v-if="card.git" target="_blank" :href="card.git" aria-label="Opens Github a new tab">
                        <img class="git-logo" src="https://cstate.se/assets/git-logo.png" alt="Image">
                      </a>

                      <a v-if="card.linkedin" target="_blank" :href="card.linkedin" aria-label="Opens LinkedIn a new tab">
                        <img class="git-logo" src="https://cstate.se/assets/linkedin-logo.png" alt="Image">
                      </a>
                      <a v-if="card.cv" target="_blank" :href="card.cv" aria-label="Opens CV a new tab">
                        <img class="git-logo" src="https://cstate.se/assets/cv-logo8.png" alt="Image">
                      </a>
                    </p>
                  </div>
                </div>

                <div class="main-description">
                  <p v-html="card.description"></p>
                </div>
                <div v-for="item in card.content">
                  <div v-if="item.id === 'overview'" class="right-img">
                    <img :src="item.img" :alt="item.caption">
                    <p v-html="item.caption"></p>
                  </div>

                  <div v-if="item.id === 'field-research'" class="left-img">
                    <img :src="item.img" :alt="item.caption">
                    <p v-html="item.caption"></p>
                  </div>

                  <div v-if="item.id === 'prototyping'" class="right-img">
                    <img :src="item.img" :alt="item.caption">
                    <p v-html="item.caption"></p>
                  </div>

                  <div v-if="item.id === 'visual'" class="left-img">
                    <img :src="item.img" :alt="item.caption">
                    <p v-html="item.caption"></p>
                  </div>

                  <div v-if="item.id === 'other'" class="other">
                    <div v-html="item.html"></div>
                    <p v-html="item.caption"></p>
                  </div>
                  <div v-if="item.id === 'other'" class="right-img">
                    <img :src="item.img" :alt="item.caption">
                  </div>

                  <!--<div :id="item.id" v-html="item.content"></div>-->
                </div>
              </div>
            </div>
          </div>
        </div>
      </a>
    </section>
    <section v-else>
      <a
        href="#"
        class="Card"
        v-for="(card,index) in items"
        v-if="index <= 0"
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
              <br />
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
              <AppHeader v-if="transitionIndex !== null && transitioning" />

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
                  <img :src="card.cover" :alt="card.heading">
                  <h1 v-html="card.heading"></h1>
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
                    <a v-if="card.url" target="_blank" :href="card.url" aria-label="Opens hte project a new tab">Go to project</a>
                    <p>
                      <a v-if="card.git" target="_blank" :href="card.git" aria-label="Opens Github a new tab">
                        <img class="git-logo" src="https://cstate.se/assets/git-logo.png" alt="Github">
                      </a>

                      <a v-if="card.linkedin" target="_blank" :href="card.linkedin" aria-label="Opens Linkedin a new tab">
                        <img class="git-logo" src="https://cstate.se/assets/linkedin-logo.png" alt="Linkedin">
                      </a>
                      <a v-if="card.cv" target="_blank" :href="card.cv" aria-label="Opens CV a new tab">
                        <img class="git-logo" src="https://cstate.se/assets/cv-logo8.png" alt="CV">
                      </a>
                    </p>
                  </div>
                </div>

                <div class="main-description">
                  <p v-html="card.description"></p>
                </div>
                <div v-for="item in card.content">
                  <div v-if="item.id === 'overview'" class="right-img">
                    <img :src="item.img" :alt="item.caption">
                    <p v-html="item.caption"></p>
                  </div>

                  <div v-if="item.id === 'field-research'" class="left-img">
                    <img :src="item.img" :alt="item.caption">
                    <p v-html="item.caption"></p>
                  </div>

                  <div v-if="item.id === 'prototyping'" class="right-img">
                    <img :src="item.img" :alt="item.caption">
                    <p v-html="item.caption"></p>
                  </div>

                  <div v-if="item.id === 'visual'" class="left-img">
                    <img :src="item.img" :alt="item.caption">
                    <p v-html="item.caption"></p>
                  </div>

                  <div v-if="item.id === 'other'" class="other">
                    <div v-html="item.html"></div>
                    <p v-html="item.caption"></p>
                  </div>
                  <div v-if="item.id === 'other'" class="right-img">
                    <img :src="item.img" :alt="item.caption">
                  </div>

                  <!--<div :id="item.id" v-html="item.content"></div>-->
                </div>
              </div>
            </div>
          </div>
        </div>
      </a>
    </section>

    <div class="FooterWrapperClass">
      <div class="Footer__FooterWrapper">
        <div class="Footer__FooterTop">
          <p>Got a project?</p>
          <h2>Let's talk.</h2>
          <a href="mailto:hej@cstate.se">Tell me everything</a>
        </div>
        <div class="Footer__FooterBottom">
          <div class="Footer__SocialLinks">
            <a href="https://github.com/statecs">
              <svg
                alt="github logo"
                role="img"
                viewBox="0 0 24 24"
                xmlns="http://www.w3.org/2000/svg"
              >
                <title>GitHub icon</title>
                <path
                  d="M12 .297c-6.63 0-12 5.373-12 12 0 5.303 3.438 9.8 8.205 11.385.6.113.82-.258.82-.577 0-.285-.01-1.04-.015-2.04-3.338.724-4.042-1.61-4.042-1.61C4.422 18.07 3.633 17.7 3.633 17.7c-1.087-.744.084-.729.084-.729 1.205.084 1.838 1.236 1.838 1.236 1.07 1.835 2.809 1.305 3.495.998.108-.776.417-1.305.76-1.605-2.665-.3-5.466-1.332-5.466-5.93 0-1.31.465-2.38 1.235-3.22-.135-.303-.54-1.523.105-3.176 0 0 1.005-.322 3.3 1.23.96-.267 1.98-.399 3-.405 1.02.006 2.04.138 3 .405 2.28-1.552 3.285-1.23 3.285-1.23.645 1.653.24 2.873.12 3.176.765.84 1.23 1.91 1.23 3.22 0 4.61-2.805 5.625-5.475 5.92.42.36.81 1.096.81 2.22 0 1.606-.015 2.896-.015 3.286 0 .315.21.69.825.57C20.565 22.092 24 17.592 24 12.297c0-6.627-5.373-12-12-12"
                />
              </svg>
            </a>
            <a href="https://www.linkedin.com/in/state">
              <img
                src="data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiPz4KPHN2ZyB3aWR0aD0iMTZweCIgaGVpZ2h0PSIxNnB4IiB2aWV3Qm94PSIwIDAgMTYgMTYiIHZlcnNpb249IjEuMSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIiB4bWxuczp4bGluaz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94bGluayI+CiAgICA8IS0tIEdlbmVyYXRvcjogU2tldGNoIDUyLjYgKDY3NDkxKSAtIGh0dHA6Ly93d3cuYm9oZW1pYW5jb2RpbmcuY29tL3NrZXRjaCAtLT4KICAgIDx0aXRsZT5sb2dvLWxpbmtlZGluPC90aXRsZT4KICAgIDxkZXNjPkNyZWF0ZWQgd2l0aCBTa2V0Y2guPC9kZXNjPgogICAgPGcgaWQ9IlN5bWJvbHMiIHN0cm9rZT0ibm9uZSIgc3Ryb2tlLXdpZHRoPSIxIiBmaWxsPSJub25lIiBmaWxsLXJ1bGU9ImV2ZW5vZGQiPgogICAgICAgIDxnIGlkPSJGb290ZXIiIHRyYW5zZm9ybT0idHJhbnNsYXRlKC03MTIuMDAwMDAwLCAtMzAzLjAwMDAwMCkiIGZpbGw9IiNBOUE5QTkiIGZpbGwtcnVsZT0ibm9uemVybyI+CiAgICAgICAgICAgIDxnIGlkPSJHcm91cC01Ij4KICAgICAgICAgICAgICAgIDxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKDU1Mi4wMDAwMDAsIDMwMy4wMDAwMDApIj4KICAgICAgICAgICAgICAgICAgICA8ZyBpZD0ibG9nby1saW5rZWRpbiIgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoMTYwLjAwMDAwMCwgMC4wMDAwMDApIj4KICAgICAgICAgICAgICAgICAgICAgICAgPHBhdGggZD0iTTE1LjMzMzMzMzMsMCBMMC42NjY2NjY2NjcsMCBDMC4yNjY2NjY2NjcsMCAwLDAuMjY2NjY2NjY3IDAsMC42NjY2NjY2NjcgTDAsMTUuMzMzMzMzMyBDMCwxNS43MzMzMzMzIDAuMjY2NjY2NjY3LDE2IDAuNjY2NjY2NjY3LDE2IEwxNS4zMzMzMzMzLDE2IEMxNS43MzMzMzMzLDE2IDE2LDE1LjczMzMzMzMgMTYsMTUuMzMzMzMzMyBMMTYsMC42NjY2NjY2NjcgQzE2LDAuMjY2NjY2NjY3IDE1LjczMzMzMzMsMCAxNS4zMzMzMzMzLDAgWiBNNC43MzMzMzMzMywxMy42NjY2NjY3IEwyLjQsMTMuNjY2NjY2NyBMMi40LDYgTDQuOCw2IEw0LjgsMTMuNjY2NjY2NyBMNC43MzMzMzMzMywxMy42NjY2NjY3IFogTTMuNTMzMzMzMzMsNC45MzMzMzMzMyBDMi44LDQuOTMzMzMzMzMgMi4xMzMzMzMzMyw0LjMzMzMzMzMzIDIuMTMzMzMzMzMsMy41MzMzMzMzMyBDMi4xMzMzMzMzMywyLjggMi43MzMzMzMzMywyLjEzMzMzMzMzIDMuNTMzMzMzMzMsMi4xMzMzMzMzMyBDNC4yNjY2NjY2NywyLjEzMzMzMzMzIDQuOTMzMzMzMzMsMi43MzMzMzMzMyA0LjkzMzMzMzMzLDMuNTMzMzMzMzMgQzQuOTMzMzMzMzMsNC4zMzMzMzMzMyA0LjMzMzMzMzMzLDQuOTMzMzMzMzMgMy41MzMzMzMzMyw0LjkzMzMzMzMzIFogTTEzLjY2NjY2NjcsMTMuNjY2NjY2NyBMMTEuMjY2NjY2NywxMy42NjY2NjY3IEwxMS4yNjY2NjY3LDkuOTMzMzMzMzMgQzExLjI2NjY2NjcsOS4wNjY2NjY2NyAxMS4yNjY2NjY3LDcuOTMzMzMzMzMgMTAuMDY2NjY2Nyw3LjkzMzMzMzMzIEM4LjgsNy45MzMzMzMzMyA4LjY2NjY2NjY3LDguODY2NjY2NjcgOC42NjY2NjY2Nyw5Ljg2NjY2NjY3IEw4LjY2NjY2NjY3LDEzLjY2NjY2NjcgTDYuMjY2NjY2NjcsMTMuNjY2NjY2NyBMNi4yNjY2NjY2Nyw2IEw4LjUzMzMzMzMzLDYgTDguNTMzMzMzMzMsNy4wNjY2NjY2NyBDOC44NjY2NjY2Nyw2LjQ2NjY2NjY3IDkuNiw1Ljg2NjY2NjY3IDEwLjgsNS44NjY2NjY2NyBDMTMuMiw1Ljg2NjY2NjY3IDEzLjY2NjY2NjcsNy40NjY2NjY2NyAxMy42NjY2NjY3LDkuNTMzMzMzMzMgTDEzLjY2NjY2NjcsMTMuNjY2NjY2NyBaIiBpZD0iU2hhcGUiPjwvcGF0aD4KICAgICAgICAgICAgICAgICAgICA8L2c+CiAgICAgICAgICAgICAgICA8L2c+CiAgICAgICAgICAgIDwvZz4KICAgICAgICA8L2c+CiAgICA8L2c+Cjwvc3ZnPg=="
                alt="linkedin logo"
              />
            </a>
            <a href="https://www.instagram.com/cstate">
              <img
                src="data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiPz4KPHN2ZyB3aWR0aD0iMTZweCIgaGVpZ2h0PSIxNnB4IiB2aWV3Qm94PSIwIDAgMTYgMTYiIHZlcnNpb249IjEuMSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIiB4bWxuczp4bGluaz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94bGluayI+CiAgICA8IS0tIEdlbmVyYXRvcjogU2tldGNoIDUyLjYgKDY3NDkxKSAtIGh0dHA6Ly93d3cuYm9oZW1pYW5jb2RpbmcuY29tL3NrZXRjaCAtLT4KICAgIDx0aXRsZT5sb2dvLWluc3RhZ3JhbTwvdGl0bGU+CiAgICA8ZGVzYz5DcmVhdGVkIHdpdGggU2tldGNoLjwvZGVzYz4KICAgIDxnIGlkPSJTeW1ib2xzIiBzdHJva2U9Im5vbmUiIHN0cm9rZS13aWR0aD0iMSIgZmlsbD0ibm9uZSIgZmlsbC1ydWxlPSJldmVub2RkIj4KICAgICAgICA8ZyBpZD0iRm9vdGVyIiB0cmFuc2Zvcm09InRyYW5zbGF0ZSgtNTkyLjAwMDAwMCwgLTMwMy4wMDAwMDApIiBmaWxsPSIjQTlBOUE5Ij4KICAgICAgICAgICAgPGcgaWQ9Ikdyb3VwLTUiPgogICAgICAgICAgICAgICAgPGcgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoNTUyLjAwMDAwMCwgMzAzLjAwMDAwMCkiPgogICAgICAgICAgICAgICAgICAgIDxnIGlkPSJsb2dvLWluc3RhZ3JhbSIgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoNDAuMDAwMDAwLCAwLjAwMDAwMCkiPgogICAgICAgICAgICAgICAgICAgICAgICA8cGF0aCBkPSJNOCwxLjQ0MTUgQzEwLjEzNiwxLjQ0MTUgMTAuMzg5LDEuNDQ5NSAxMS4yMzI1LDEuNDg4IEMxMi4xNDMsMS41Mjk1IDEyLjk4OCwxLjcxMiAxMy42MzgsMi4zNjIgQzE0LjI4OCwzLjAxMiAxNC40NzA1LDMuODU3IDE0LjUxMiw0Ljc2NzUgQzE0LjU1MDUsNS42MTEgMTQuNTU4NSw1Ljg2NCAxNC41NTg1LDggQzE0LjU1ODUsMTAuMTM2IDE0LjU1MDUsMTAuMzg5IDE0LjUxMiwxMS4yMzI1IEMxNC40NzA1LDEyLjE0MyAxNC4yODgsMTIuOTg4IDEzLjYzOCwxMy42MzggQzEyLjk4OCwxNC4yODggMTIuMTQzLDE0LjQ3MDUgMTEuMjMyNSwxNC41MTIgQzEwLjM4OSwxNC41NTA1IDEwLjEzNiwxNC41NTg1IDgsMTQuNTU4NSBDNS44NjQsMTQuNTU4NSA1LjYxMSwxNC41NTA1IDQuNzY3NSwxNC41MTIgQzMuODU3LDE0LjQ3MDUgMy4wMTIsMTQuMjg4IDIuMzYyLDEzLjYzOCBDMS43MTIsMTIuOTg4IDEuNTI5NSwxMi4xNDMgMS40ODgsMTEuMjMyNSBDMS40NDk1LDEwLjM4OSAxLjQ0MTUsMTAuMTM2IDEuNDQxNSw4IEMxLjQ0MTUsNS44NjQgMS40NDk1LDUuNjExIDEuNDg4LDQuNzY3NSBDMS41Mjk1LDMuODU3IDEuNzEyLDMuMDEyIDIuMzYyLDIuMzYyIEMzLjAxMiwxLjcxMiAzLjg1NywxLjUyOTUgNC43Njc1LDEuNDg4IEM1LjYxMSwxLjQ0OTUgNS44NjQsMS40NDE1IDgsMS40NDE1IFogTTgsMCBDNS44Mjc1LDAgNS41NTUsMC4wMDkgNC43MDE1LDAuMDQ4IEMzLjQwMTUsMC4xMDc1IDIuMjU5NSwwLjQyNiAxLjM0MjUsMS4zNDI1IEMwLjQyNiwyLjI1OSAwLjEwNzUsMy40MDEgMC4wNDgsNC43MDE1IEMwLjAwOSw1LjU1NSAwLDUuODI3NSAwLDggQzAsMTAuMTcyNSAwLjAwOSwxMC40NDUgMC4wNDgsMTEuMjk4NSBDMC4xMDc1LDEyLjU5ODUgMC40MjYsMTMuNzQwNSAxLjM0MjUsMTQuNjU3NSBDMi4yNTksMTUuNTc0IDMuNDAxLDE1Ljg5MjUgNC43MDE1LDE1Ljk1MiBDNS41NTUsMTUuOTkxIDUuODI3NSwxNiA4LDE2IEMxMC4xNzI1LDE2IDEwLjQ0NSwxNS45OTEgMTEuMjk4NSwxNS45NTIgQzEyLjU5ODUsMTUuODkyNSAxMy43NDA1LDE1LjU3NCAxNC42NTc1LDE0LjY1NzUgQzE1LjU3NCwxMy43NDEgMTUuODkyNSwxMi41OTkgMTUuOTUyLDExLjI5ODUgQzE1Ljk5MSwxMC40NDUgMTYsMTAuMTcyNSAxNiw4IEMxNiw1LjgyNzUgMTUuOTkxLDUuNTU1IDE1Ljk1Miw0LjcwMTUgQzE1Ljg5MjUsMy40MDE1IDE1LjU3NCwyLjI1OTUgMTQuNjU3NSwxLjM0MjUgQzEzLjc0MSwwLjQyNiAxMi41OTksMC4xMDc1IDExLjI5ODUsMC4wNDggQzEwLjQ0NSwwLjAwOSAxMC4xNzI1LDAgOCwwIFoiIGlkPSJTaGFwZSIgZmlsbC1ydWxlPSJub256ZXJvIj48L3BhdGg+CiAgICAgICAgICAgICAgICAgICAgICAgIDxwYXRoIGQ9Ik04LDMuODkyIEM1LjczMSwzLjg5MiAzLjg5Miw1LjczMTUgMy44OTIsOCBDMy44OTIsMTAuMjY5IDUuNzMxNSwxMi4xMDggOCwxMi4xMDggQzEwLjI2ODUsMTIuMTA4IDEyLjEwOCwxMC4yNjg1IDEyLjEwOCw4IEMxMi4xMDgsNS43MzEgMTAuMjY5LDMuODkyIDgsMy44OTIgWiBNOCwxMC42NjY1IEM2LjUyNywxMC42NjY1IDUuMzMzNSw5LjQ3MjUgNS4zMzM1LDggQzUuMzMzNSw2LjUyNyA2LjUyNzUsNS4zMzM1IDgsNS4zMzM1IEM5LjQ3Myw1LjMzMzUgMTAuNjY2NSw2LjUyNzUgMTAuNjY2NSw4IEMxMC42NjY1LDkuNDczIDkuNDczLDEwLjY2NjUgOCwxMC42NjY1IFoiIGlkPSJTaGFwZSIgZmlsbC1ydWxlPSJub256ZXJvIj48L3BhdGg+CiAgICAgICAgICAgICAgICAgICAgICAgIDxjaXJjbGUgaWQ9Ik92YWwiIGN4PSIxMi4yNzA1IiBjeT0iMy43Mjk1IiByPSIxIj48L2NpcmNsZT4KICAgICAgICAgICAgICAgICAgICA8L2c+CiAgICAgICAgICAgICAgICA8L2c+CiAgICAgICAgICAgIDwvZz4KICAgICAgICA8L2c+CiAgICA8L2c+Cjwvc3ZnPg=="
                alt="instagram logo"
              />
            </a>
            <a href="https://twitter.com/statecs">
              <img
                src="data:image/svg+xml;base64,PD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0iVVRGLTgiPz4KPHN2ZyB3aWR0aD0iMTZweCIgaGVpZ2h0PSIxNHB4IiB2aWV3Qm94PSIwIDAgMTYgMTQiIHZlcnNpb249IjEuMSIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIiB4bWxuczp4bGluaz0iaHR0cDovL3d3dy53My5vcmcvMTk5OS94bGluayI+CiAgICA8IS0tIEdlbmVyYXRvcjogU2tldGNoIDUyLjYgKDY3NDkxKSAtIGh0dHA6Ly93d3cuYm9oZW1pYW5jb2RpbmcuY29tL3NrZXRjaCAtLT4KICAgIDx0aXRsZT5sb2dvLXR3aXR0ZXI8L3RpdGxlPgogICAgPGRlc2M+Q3JlYXRlZCB3aXRoIFNrZXRjaC48L2Rlc2M+CiAgICA8ZyBpZD0iU3ltYm9scyIgc3Ryb2tlPSJub25lIiBzdHJva2Utd2lkdGg9IjEiIGZpbGw9Im5vbmUiIGZpbGwtcnVsZT0iZXZlbm9kZCI+CiAgICAgICAgPGcgaWQ9IkZvb3RlciIgdHJhbnNmb3JtPSJ0cmFuc2xhdGUoLTYzMi4wMDAwMDAsIC0zMDQuMDAwMDAwKSIgZmlsbD0iI0E5QTlBOSI+CiAgICAgICAgICAgIDxnIGlkPSJHcm91cC01Ij4KICAgICAgICAgICAgICAgIDxnIHRyYW5zZm9ybT0idHJhbnNsYXRlKDU1Mi4wMDAwMDAsIDMwMy4wMDAwMDApIj4KICAgICAgICAgICAgICAgICAgICA8ZyBpZD0ibG9nby10d2l0dGVyIiB0cmFuc2Zvcm09InRyYW5zbGF0ZSg4MC4wMDAwMDAsIDEuMDAwMDAwKSI+CiAgICAgICAgICAgICAgICAgICAgICAgIDxwYXRoIGQ9Ik0xNiwyIEMxNS40LDIuMyAxNC44LDIuNCAxNC4xLDIuNSBDMTQuOCwyLjEgMTUuMywxLjUgMTUuNSwwLjcgQzE0LjksMS4xIDE0LjIsMS4zIDEzLjQsMS41IEMxMi44LDAuOSAxMS45LDAuNSAxMSwwLjUgQzkuMywwLjUgNy44LDIgNy44LDMuOCBDNy44LDQuMSA3LjgsNC4zIDcuOSw0LjUgQzUuMiw0LjQgMi43LDMuMSAxLjEsMS4xIEMwLjgsMS42IDAuNywyLjEgMC43LDIuOCBDMC43LDMuOSAxLjMsNC45IDIuMiw1LjUgQzEuNyw1LjUgMS4yLDUuMyAwLjcsNS4xIEMwLjcsNS4xIDAuNyw1LjEgMC43LDUuMSBDMC43LDYuNyAxLjgsOCAzLjMsOC4zIEMzLDguNCAyLjcsOC40IDIuNCw4LjQgQzIuMiw4LjQgMiw4LjQgMS44LDguMyBDMi4yLDkuNiAzLjQsMTAuNiA0LjksMTAuNiBDMy44LDExLjUgMi40LDEyIDAuOCwxMiBDMC41LDEyIDAuMywxMiAwLDEyIEMxLjUsMTIuOSAzLjIsMTMuNSA1LDEzLjUgQzExLDEzLjUgMTQuMyw4LjUgMTQuMyw0LjIgQzE0LjMsNC4xIDE0LjMsMy45IDE0LjMsMy44IEMxNSwzLjMgMTUuNiwyLjcgMTYsMiBaIiBpZD0iUGF0aCI+PC9wYXRoPgogICAgICAgICAgICAgICAgICAgIDwvZz4KICAgICAgICAgICAgICAgIDwvZz4KICAgICAgICAgICAgPC9nPgogICAgICAgIDwvZz4KICAgIDwvZz4KPC9zdmc+"
                alt="twitter logo"
              />
            </a>
          </div>
          <p class="Footer__Copyright">Designed with ♥ in Stockholm, Sweden</p>
        </div>
      </div>
    </div>
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
      showProjects: false,
      toggled: false,
      title: "Featured Articles",
      transitioning: false,
      transitionIndex: null,
      transitionFixedIndex: null,
      items: [
        {
          id: "1",
          message: "Christopher State",
          heading: "Christopher",
          title: "Design Technologist",
          subtitle: "Accessibility, UX, Figma, JavaScript",
          tech: "Accessibility, UX, Figma, JavaScript",
          year: "1993- ",
          git: "https://github.com/statecs",
          linkedin: "https://linkedin.com/in/state",
          cv: "https://cstate.se/assets/cv.pdf",
          description:
            "Burning passion in creating solutions that makes a difference. I am a highly motivated and enthusiastic student with a genuine interest in web and media technologies. Ever since I learn to code from the age sixteen, I have been driven, curious and spent most of my education career broadening my knowledge. My personal goal include exploring new thinking while pushing the limits of what is possible.",
          content: [
            {
              id: "overview",
              img: "https://cstate.se/images/chris-1.jpg",
              caption:
                "Sep 2004 | I have always been interested in new technology. I quickly became the guy who helped friends and friends parents with everything related to IT. These skills helped me make my first money from a young age which kept me motivated. Browsing the internet in order to find solutions become the foundation of my problem solving."
            },
            {
              id: "field-research",
              img: "https://cstate.se/images/chris-2.jpg",
              caption:
                "Feb 2015 - Feb 2016 | I worked together with an amazing project team at THS Armada which arranges Scandinavia's largest career fair at KTH Royal Institute of Technology. The role included leading and supporting the developers and the managament team and to build momentum within the group"
            },
            {
              id: "prototyping",
              img: "https://cstate.se/images/chris-3.jpg",
              caption:
                "Oct 2016 - Aug 2019 | Traveling around Sweden to represent KTH at fairs, events and high schools. Inform presumptive students about higher education, career options and opportunities after high school in general and KTH in particular."
            },
            {
              id: "visual",
              img: "https://cstate.se/images/chris-4.jpg",
              caption: ""
            },
            {
              id: "prototyping",
              img: "https://cstate.se/images/chris-5.jpg",
              caption:
                "Jun 2017 - Jun 2018 | Head of Communications at THS, representing students at the Royal Institute of Technology in Stockholm. THS is one of Sweden’s oldest student unions and has over 112 years of experience in working for students’ rights at KTH. "
            },
            {
              id: "visual",
              img: "https://cstate.se/images/chris-6.jpg",
              caption:
                "Oct 2017 - Aug 2018 | Studs, or the Study Trip, is an annual project at the Department of Computer Science at the Royal Institute of Technology (KTH) in Stockholm. The project aims to create a platform for interaction between students close to graduation and relevant companies. The project ends with a study trip to give the students an opportunity to meet companies abroad."
            },
            {
              id: "prototyping",
              img: "",
              caption: ""
            }
          ],
          cover: "https://cstate.se/images/chris-placeholder.jpg",
          author: {
            name: "State",
            image: ""
          }
        },
        {
          id: "2",
          message: "ICA",
          heading: "ICA",
          title: "UX/UI Designer | ICA Gruppen AB",
          subtitle: "Figma, Accessibility | Mar 2022 - Present",
          tech: "Figma, Accessibility",
          year: "March 2022 - Present",
          url: "https://docs.google.com/presentation/d/1YoiQnn62IJwq0lRxo3YPTXf4kWqJLRsXmlOPXd4DXA4/edit?usp=sharing",
          description:
            "With great commitment and the latest technology, we develop better solutions to improve the everyday life of all our customers.",
          content: [
            {
              id: "overview",
              img: "https://cstate.se/images/ica-1.jpg",
              caption:
                "Color palette for the new design"
            },
            {
              id: "field-research",
              img: "https://cstate.se/images/ica-2.jpg",
              caption:
                "Typography"
            },
            {
              id: "prototyping",
              img: "https://cstate.se/images/ica-3.jpg",
              caption:
                "Resuable components built in Figma"
            },
            {
              id: "visual",
              img: "https://cstate.se/images/ica-4.jpg",
              caption:
                "Mobile sketches for the intranet for ICA.se"
            },
            {
              id: "prototyping",
              img: "",
              caption: ""
            }
          ],
          cover: "https://cstate.se/images/ica-placeholder-1.jpg",
          author: {
            name: "ica",
            image: ""
          }
        },
        {
          id: "3",
          message: "Mapiful",
          heading: "Mapiful",
          title: "UX Developer | Mapiful",
          subtitle: "Vue, Wordpress, Figma | Jan 2021 - Mar 2022",
          tech: "Vue, Wordpress, Figma",
          year: "January 2021 - March 2022",
          url: "https://www.mapiful.com/",
          figma: "https://www.figma.com/file/N7g4rP7M9kWoqm2A6QcBJd/Mapiful?node-id=1347%3A813",
          description:
            "Mapiful provides the technology to let you choose from any place in the world and design your own unique map print. Explore, zoom, customize and order. Voila, your place of birth, favorite neighborhood or just your happy place framed on your wall, in your home. Making sure the UX is top-notch on the site, identifying pain points and easy-wins, looking through support tickets, and investigating any potential issues on the site. Product/front-end development, working closely with the product team, adding new features to the editors, sourcing new illustrations to line-art editors, and other front-end development tasks of the site.",
          content: [
            {
              id: "overview",
              img: "https://cstate.se/images/mapiful-1.jpg",
              caption:
                "Responsible for Figma, components, and brand colors of Mapiful."
            },
            {
              id: "field-research",
              img: "https://cstate.se/images/mapiful-2.jpg",
              caption:
                "Responsible for Figma, components, and brand colors of Mapiful. "
            },
            {
              id: "prototyping",
              img: "https://cstate.se/images/mapiful-3.jpg",
              caption:
                "Inspirational moodboard for the redesign of the website"
            },
            {
              id: "visual",
              img: "https://cstate.se/images/mapiful-5.jpg",
              caption:
                "Hero design"
            },
            {
              id: "prototyping",
              img: "https://cstate.se/images/mapiful-7.jpg",
              caption: "Final design of the frontpage"
            },
            {
              id: "visual",
              img: "",
              caption:
                ""
            },
          ],
          cover: "https://cstate.se/images/mapiful-placeholder-2.jpg",
          author: {
            name: "mapiful",
            image: ""
          }
        },
        {
          id: "4",
          message: "Designing Conversational AI in digital healthcare in regards to accessibility",
          heading: "AI Chatbot",
          title: "Master Thesis | Course: DA232X",
          subtitle: "React, Python, Sketch | Jan 2020 - Jun 2020",
          tech: "React, Python, Sketch",
          year: "January 2020 - June 2020",
          url: "https://docs.google.com/presentation/d/1HkI-JAr0iQPheC5lUyoevX6McbsQLt3Cu7HGFTdvoKU/edit?usp=sharing",
          git: "https://github.com/statecs/aida",
          description:
            "A prototype was designed and built using ReactJs together with Python using Rasa - Natural Language Understanding. Several a11y-tools for accessibility were used while building the prototype. The accessibility tools included screen readers, and different a11y tools integrated in visual studio code. The prototype was also evaluated in regards to the ISO Standard 21801-1:2020 – Cognitive Accessibility",
          content: [
            {
              id: "overview",
              img: "https://cstate.se/images/exjobb-0_1.jpg",
              caption:
                  "Chatbots only know limited answers. They may not always be the best approach but they can answer basic questions which is very helpful. In cases when the chatbot is unaware of an answer, it should redirect to a real doctor."
            },  
            {
              id: "field-research",
              img: "https://cstate.se/images/exjobb-0_2.jpg",
              caption:
                  "BankID was one of the biggest limitations today, because people with disabilities often need a god man, which is not accepted by BankID."
            }, 
            {
              id: "overview",
              img: "https://cstate.se/images/exjobb-1_1.jpg",
              caption:
                "Moodboard in the first ideation phase. Keywords: Online symtom checkers, digital health chatbots and accessibility."
            },
            {
              id: "field-research",
              img: "https://cstate.se/images/exjobb-2_1.jpg",
              caption:
                "Sketching on the first iteration of the prototype based on the moodboard and inspiration from Typeform and other digital health chatbots."
            },
            {
              id: "prototyping",
              img: "https://cstate.se/images/exjobb-3_1.jpg",
              caption:
                "Prototype made in Framer X and tested together with Begripsam in order to evaluate ISO Standard 21801-1:2020 – Cognitive Accessibility"
            },
            {
              id: "visual",
              img: "https://cstate.se/images/exjobb-4_1.jpg",
              caption:
                "Final version developed in React"
            },
            {
              id: "prototyping",
              img: "",
              caption: ""
            }
          ],
          cover: "https://cstate.se/images/exjobb-placeholder-5.jpg",
          author: {
            name: "exjobb",
            image: ""
          }
        },
        {
          id: "5",
          message: "Studs - Studieresan",
          heading: "Studs",
          title: "Art Director | Course: AI2151",
          subtitle: "Sketch, InDesign | Oct 2017 - Aug 2018",
          tech: "Sketch, InDesign",
          year: "October 2017 - August 2018",
          url: "https://studieresan.se",
          description:
            "Studs, or the Study Trip, is an annual project at the Department of Computer Science at the Royal Institute of Technology (KTH) in Stockholm. The project aims to create a platform for interaction between students close to graduation and relevant companies. The project ends with a study trip to give the students an opportunity to meet companies abroad. The report itself serves as the major delivery in the course, serving as a record of the project.",
          content: [
            {
              id: "overview",
              img: "https://cstate.se/images/studs-1.jpg",
              caption: "Moodboard in the first ideation phase."
            },
            {
              id: "field-research",
              img: "https://cstate.se/images/studs-2.jpg",
              caption: "First iteration of the layout."
            },
            {
              id: "prototyping",
              img: "https://cstate.se/images/studs-3.jpg",
              caption: "Final layout"
            },
            {
              id: "visual",
              img: "https://cstate.se/images/studs-4.jpg",
              caption: ""
            },
            {
              id: "other",
              html:
                "<br /><a style='color: #42b983;' href='https://drive.google.com/file/d/1X8-gNNXPlpWrLF4Uf1I9xj2caoDKi7ws/view?usp=sharing'>Link to report </a> <br />",
              caption: ""
            }
          ],
          cover: "https://cstate.se/images/studs-placeholder.jpg",
          author: {
            name: "Studs",
            image: ""
          }
        },
        {
          id: "6",
          message: "THS Website",
          heading: "THS Web",
          title: "Front-end Developer",
          subtitle: "Angular, WP REST | 2017 - 2019",
          tech: "Angular, WP REST",
          year: "2017 - 2019",
          url: "https://ths.kth.se",
          git: "https://github.com/thskth",
          description:
            "Rebuilt from scratch using latest technologies in Angular and WP REST. Project with two people where my responsibilities included project lead, UX Design and front-end development. Also, during my year as Head of Communcations I created a new graphical identitiy for THS.",
          content: [
            {
              id: "overview",
              img: "https://cstate.se/images/ths-1.jpg",
              caption: "Updated logo with a more modern look and feeling."
            },
            {
              id: "field-research",
              img: "https://cstate.se/images/ths-2.jpg",
              caption:
                "New graphical material that follow the graphical identity."
            },
            {
              id: "prototyping",
              img: "https://cstate.se/images/ths-3.jpg",
              caption: "Sketch mockups on different views (Desktop)"
            },
            {
              id: "visual",
              img: "https://cstate.se/images/ths-4.jpg",
              caption: "Sketch mockups on different views (Mobile)"
            },
            {
              id: "prototyping",
              img: "https://cstate.se/images/ths-5.jpg",
              caption: "Adaptable homepage depending on your interests."
            },
            {
              id: "visual",
              img: "https://cstate.se/images/ths-6.jpg",
              caption:
                "Chatbot integrated in order to enhance the service from the Student Union Office. "
            },
            {
              id: "prototyping",
              img: "https://cstate.se/images/ths-7.jpg",
              caption: "Full-page screenshot"
            },
            {
              id: "other",
              html: ""
            }
          ],
          cover: "https://cstate.se/images/ths-placeholder.jpg",
          author: {
            name: "THS",
            image: ""
          }
        },
        {
          id: "7",
          message: "CreativeStudio",
          heading: "Creative",
          title: "UX Designer",
          subtitle: "Wordpress, Javascript | Aug 2018",
          tech: "Wordpress, Javascript",
          year: "August 2018",
          url: "",
          description:
            "Creative Studio is a family owned studio for children to get acquainted with basic singing techniques, play and sing simpler songs of different music styles.",
          content: [
            {
              id: "overview",
              img: "https://cstate.se/images/creativestudio-1.jpg",
              caption: "Graphical identity and color palette. "
            },
            {
              id: "field-research",
              img: "https://cstate.se/images/creativestudio-2.jpg",
              caption: "Low-fi prototype."
            },
            {
              id: "prototyping",
              img: "https://cstate.se/images/creativestudio-3.jpg",
              caption: ""
            },
            {
              id: "visual",
              img: "https://cstate.se/images/creativestudio-4.jpg",
              caption: "Website developed in Wordpress"
            }
          ],
          cover: "https://cstate.se/images/creativestudio-placeholder.jpg",
          author: {
            name: "Creativestudio",
            image: ""
          }
        },
        {
          id: "8",
          message: "Gameful self-directed learning",
          heading: "Gameful",
          title: "Designer | Course: DM2799",
          subtitle: "inVision Studio | Dec 2018",
          tech: "UI/ UX",
          year: "December 2018",
          url: "https://docs.google.com/presentation/d/1aWkK7eQPUrD8E7QbS86UjRM04wc1XqolpaQ4Ir0T3Ds/edit?usp=sharing",
          description:
            "This project was developed as part of a collaboration between KTH and Kanda University of International Studies (KUIS) in Japan. The interactive prototype has been created in inVision Studio, using gameful elements categorized into three categories, i.e., objective, progression and feedback. Objective - A behavioral mechanic type, requiring the user to take action for the reward, Progression - Move the user through the content. Feedback - Informing the user of their status.",
          content: [
            {
              id: "overview",
              img: "https://cstate.se/images/gameful-1.jpg",
              caption: "Moodboard in the first ideation phase."
            },
            {
              id: "field-research",
              img: "https://cstate.se/images/gameful-2.jpg",
              caption:
                "A prototype for a gameful self-directed learning application developed for Japanese students"
            },
            {
              id: "prototyping",
              img: "",
              caption: ""
            },
            {
              id: "visual",
              img: "",
              caption: ""
            },
            {
              id: "other",
              html:
                "<iframe width='100%' height='315' frameBorder='0' src='https://www.youtube.com/embed/PIDCoaKP2hM' frameborder='0' allow='accelerometer; autoplay; encrypted-media; gyroscope; picture-in-picture' allowfullscreen></iframe>"
            }
          ],
          cover: "https://cstate.se/images/gameful-placeholder.jpg",
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
  outline: 2px solid #42b983;  /* Custom focus indicator for buttons */
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
  content: "";
  position: absolute;
  left: 0;
  right: 0;
  top: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.15);
  transition: height 400ms ease-out 200ms;
  border-radius: 15px;
}

/* .Card:after {
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
}*/

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
.Card-body {
  z-index: 1;
}
/* .Card:active {
  -webkit-transform: scale(0.95);
  transform: scale(0.95);
}*/
.Card-header {
  z-index: 1;
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
  padding: 20px;
  position: relative;
  overflow: scroll;
  z-index: 1;
  background-color: transparent;
  position: relative;
  overflow-x: hidden;
}

.inner-content {
  padding-bottom: env(safe-area-inset-bottom); /* for iPhone X */
  border-top-left-radius: 20px;
  border-top-right-radius: 20px;
}

.details {
  font-size: 13px;
  padding-top: 50px;
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
  margin-top: -40px;
  font-size: 80px;
  color: #f3f3f3;
  margin-bottom: 80px;
  width: 150%;
  /* text-align: right;*/
  position: absolute;
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
  text-align: left;
  padding-top: 50px;
  padding-bottom: 70px;
}
.right-img img {
  max-width: 100%;
}
.main-description {
  margin-top: 30px;
}
.git-logo {
  padding: 5px;
  width: 20px;
}
.Footer__FooterTop {
  padding-top: 30px;
}
.Footer__SocialLinks {
  width: 200px;
  display: grid;
  -webkit-box-align: center;
  align-items: center;
  justify-items: center;
  grid-template-columns: repeat(5, auto);
  margin: 20px auto;
}
.Footer__SocialLinks svg {
  width: 17px;
  fill: #a9a9a9;
}
.Footer__Copyright {
  color: #767676;
  padding-bottom: 30px;
}
.hello nav a {
  color: #2c3e50;
  text-decoration: none;
}

.hello nav a svg {
  position: absolute;
  padding: 2px 5px;
  fill: #2c3e50;
  text-decoration: none;
}
.hello nav a svg.back {
  position: absolute;
  margin: -1px -30px;
  fill: #2c3e50;
  text-decoration: none;
}

@media screen and (min-width: 480px) {
  .left-first-img {
    max-width: 106%;
  }
  .left-first-img h1 {
    margin-top: -50px;
    font-size: 150px;
  }
  .inner-content {
    padding: 0 50px;
  }
}
@media screen and (min-width: 769px) {
  .details {
    padding-top: 150px;
  }
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
    font-size: 180px;
    margin-bottom: 150px;
  }
  .Card.is-active .Card-header {
    padding: 30px;
  }
  .main-description {
    float: right;
    max-width: 50%;
    margin-top: -150px;
  }
}
@media screen and (min-width: 1024px) {
  .container-content {
    max-width: 70vw;
    padding: 0px 100px;
  }
  .left-first-img img {
    max-height: 800px;
  }
  .left-first-img h1 {
    font-size: 200px;
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
@media screen and (min-width: 1280px) {
  .left-first-img h1 {
    font-size: 250px;
    margin-bottom: 170px;
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
  .left-first-img h1 {
    width: 60%;
  }

  .Card {
    max-width: 65vw;
    /* styles here */
  }
  .container-content {
    max-width: 50vw;
  }
}
[role="button"]:focus {
  outline: 2px solid #42b983;  /* Custom focus indicator for elements acting as buttons */
}

</style>
