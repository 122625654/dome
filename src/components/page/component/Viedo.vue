<template>
  <div class="homepage-hero-module">
    <div class="video-container">
      <div :style="fixStyle" class="filter"></div>
      <video :style="fixStyle" autoplay loop class="fillWidth" muted="muted" v-on:canplay="canplay">
        <source src="@/assets/video/oceans2.mp4" type="video/mp4"/>
        <source src="@/assets/video/oceans2.mp4" type="video/webm"/>
      </video>
    </div>
  </div>
</template>

<script>
export default {
  data: function() {
    return {
      vedioCanPlay: false,
      fixStyle: "",
    };
  },
  methods: {
    canplay() {
      this.vedioCanPlay = true;
    },
  },
  mounted: function() {
    window.onresize = () => {
      const windowWidth = document.body.clientWidth;
      const windowHeight = document.body.clientHeight;
      const windowAspectRatio = windowHeight / windowWidth;
      let videoWidth;
      let videoHeight;
      if (windowAspectRatio < 0.5625) {
        videoWidth = windowWidth;
        videoHeight = videoWidth * 0.5625;
        this.fixStyle = {
          height: windowWidth * 0.5625 + "px",
          width: windowWidth + "px",
          "margin-bottom": (windowHeight - videoHeight) / 2 + "px",
          "margin-left": "initial",
        };
      } else {
        videoHeight = windowHeight;
        videoWidth = videoHeight / 0.5625;
        this.fixStyle = {
          height: windowHeight + "px",
          width: windowHeight / 0.5625 + "px",
          "margin-left": (windowWidth - videoWidth) / 2 + "px",
          "margin-bottom": "initial",
        };
      }
    };
    window.onresize();
  },
};
</script>

<style scoped>
.homepage-hero-module,
.video-container {
  position: relative;
  height: 100%;
  overflow: hidden;
}

.video-container .poster img,
.video-container video {
  z-index: 0;
  height: 100px;
  position: absolute;
}

.video-container .filter {
  z-index: 1;
  position: absolute;
  background: rgba(0, 0, 0, 0.4);
}
</style>
