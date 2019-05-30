<template>
  <div id="app">
    <hooper ref="slider"
            :infiniteScroll="true"
            :autoPlay="true"
            :playSpeed="playSpeed"
            :hoverPause="false"
            :mouseDrag="false"
    >
      <slide v-for="(slide, index) in slides" :key="index" :index="index" :duration="slide.duration">
        <!--<div style="background-color: coral; width: 200px; height: 200px;">{{slide.title}}</div>-->
        <template v-if="slide.type === 'frame'">
          <div class="outerbox">
            <iframe
              class="blockelement"
              :width="slideWidth"
              :height="slideHeight"
              sandbox="allow-same-origin allow-top-navigation allow-forms allow-scripts"
              :src="slide.url"
              frameborder="0"
              scrolling="no"
              allowTransparency="true"
              webkitallowfullscreen
              mozallowfullscreen
              allowfullscreen
            ></iframe>
            <div class="overlaybox fallback">
              <img :width="slideWidth"
                   :height="slideHeight"
                   :src="fallbackImg"
                   class="blockelement"
                   alt="">
            </div>
          </div>
        </template>
        <template v-if="slide.type === 'image'">
          <div class="outerbox">
            <img
              class="blockelement"
              :src="slide.src"
              :width="slideWidth"
              :height="slideHeight"
              alt="image">
            <div class="overlaybox fallback">
              <img :width="slideWidth"
                   :height="slideHeight"
                   :src="fallbackImg"
                   class="blockelement"
                   alt="">
            </div>
          </div>
        </template>
      </slide>
    </hooper>
  </div>
</template>

<script>
  import axios from 'axios';
  import {Hooper, Slide} from 'hooper';
  import 'hooper/dist/hooper.css';

  // to do  - fall back image-- need to overlay under the frame.
  //        - use a vue friendly iframe
  //        - specify different config.json files
  //
  export default {
    name: 'app',
    data() {
      return {
        config: {},
        slides: [{title: "one", url: "http://www.lmax.com/"}],
        playSpeed: 5000,
        slideWidth: 200,
        slideHeight: 200,
        fallbackImg: ""
      }
    },
    components: {
      Hooper,
      Slide
    },
    created() {
      axios.get("./assets/config.json").then(response => {
        this.config = response.data;

        if (typeof this.config === "string") {
          console.error('I think this is a string. Incorrect JSON',this.config);
          alert("problem with configuration file. Usually this means invalid JSON format");
        }
        this.slides = response.data.slides;
        this.playSpeed = response.data.defaultDuration;
        this.slideWidth = response.data.width;
        this.slideHeight = response.data.height;
        this.fallbackImg = response.data.fallbackImg;
        // all the update logic in this widget is broken. Reaching deep
        // into the component to prod the right place.
        this.$refs.slider.config.playSpeed = response.data.defaultDuration;
        this.$refs.slider.timer.restart(response.data.defaultDuration);
        console.log(response);
      }).catch(error => {
        console.error(error);
        alert("problem loading configuration file. Is it correctly named and in the right folder?");
      })
    }
  }
</script>
<style>
  #app {
    margin: 0px;
    padding: 0px;
    overflow-y: scroll;
    scrollbar-width: none; /* Firefox */
    -ms-overflow-style: none;  /* IE 10+ */
  }

  #app::-webkit-scrollbar { /* WebKit */
    width: 0;
    height: 0;
  }

  body {
    margin: 0px;
    padding: 0px;
  }

  .hooper {
    height: 100%
  }

  .outerbox {
    display: block;
    position: relative;
  }

  .overlaybox {
    top: 0;
    left: 0;
    position: absolute;
    padding: 0;
  }

  .fallback {
    z-index: -1;
    border: 0;
  }

  .blockelement {
    display:block;
  }
</style>
