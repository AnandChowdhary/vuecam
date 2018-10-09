<template>
  <div>
    <video playsinline ref="cameraVideo" />
    <canvas id="cameraCanvas" ref="cameraCanvas" aria-hidden="true" />
  </div>
</template>

<script>
export default {
  data: () => {
    return {
      img: "Hello"
    };
  },
  props: ["width", "height", "facingMode"],
  mounted() {
    this.updateFeed();
  },
  computed: {
    everything() {
      return this.width, this.height, this.facingMode;
    }
  },
  watch: {
    everything() {
      this.updateFeed();
    }
  },
  methods: {
    updateFeed() {
      const constraints = {
        audio: false,
        video: {
          facingMode: this.facingMode || "user"
        }
      };
      if (this.width) this.$refs.cameraVideo.style.width = this.width + "px";
      if (this.height) this.$refs.cameraVideo.style.width = this.height + "px";
      this.$refs.cameraVideo.setAttribute("autoplay", "");
      this.$refs.cameraVideo.setAttribute("muted", "");
      this.$refs.cameraVideo.setAttribute("playsinline", "");
      navigator.mediaDevices
        .getUserMedia(constraints)
        .then(mediaStream => {
          this.$refs.cameraVideo.srcObject = mediaStream;
          this.$refs.cameraVideo.addEventListener("loadedmetadata", () => {
            this.$refs.cameraVideo.play();
          });
        })
        .catch(error => {
          console.log("Error", error);
        });
    },
    click() {
      this.$refs.cameraCanvas.width = this.$refs.cameraVideo.offsetWidth;
      this.$refs.cameraCanvas.height = this.$refs.cameraVideo.offsetHeight;
      this.$refs.cameraCanvas
        .getContext("2d")
        .drawImage(
          this.$refs.cameraVideo,
          0,
          0,
          this.$refs.cameraCanvas.width,
          this.$refs.cameraCanvas.height
        );
      return this.$refs.cameraCanvas.toDataURL();
    }
  }
};
</script>

<style scoped>
#cameraCanvas {
  display: none;
}
</style>
