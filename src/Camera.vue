<template>
  <div>
    <div>CAMERA {{img}}</div>
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
          width: this.width || 1280,
          height: this.height || 720,
          facingMode: this.facingMode || "user"
        }
      };
      this.$refs.cameraCanvas.style.width = (this.width || 1280) + "px";
      this.$refs.cameraCanvas.style.height = (this.height || 720) + "px";
      navigator.mediaDevices
        .getUserMedia(constraints)
        .then(mediaStream => {
          this.$refs.cameraVideo.srcObject = mediaStream;
          this.$refs.cameraVideo.addEventListener("loadedmetadata", () => {
            this.$refs.cameraVideo.play();
          });
        })
        .catch(error => {
          alert(JSON.stringify(error));
        });
    },
    click() {
      this.$refs.cameraCanvas
        .getContext("2d")
        .drawImage(
          this.$refs.cameraVideo,
          0,
          0,
          this.width || 1280,
          this.height || 720
        );
      return this.$refs.cameraCanvas.toDataURL();
    }
  }
};
</script>

<style scoped>
#cameraCanvas {
  position: absolute !important;
  clip: rect(1px, 1px, 1px, 1px);
  padding: 0 !important;
  border: 0 !important;
  height: 1px !important;
  width: 1px !important;
  overflow: hidden;
}
</style>
