<template>
  <div id="app">
    <div>Sample:</div>
    <Camera ref="camera" width="300" height="300" :facingMode="facingMode" />
    <button @click="clickPhoto">Click photo</button>
    <button @click="toggleFacingMode">Toggle camera</button>
    <div>Facing mode: {{facingMode}}</div>
    <div><img alt="Your image" :src="image"></div>
    <button @click="updateFeed">Force update feed</button>
  </div>
</template>

<script>
import Camera from "./Camera.vue";
export default {
  data() {
    return {
      facingMode: "user",
      image: ""
    };
  },
  components: {
    Camera
  },
  methods: {
    clickPhoto() {
      this.image = this.$refs.camera.click();
    },
    updateFeed() {
      this.image = this.$refs.camera.updateFeed();
    },
    toggleFacingMode() {
      this.facingMode = this.facingMode === "user" ? "environment" : "user";
    }
  }
};
</script>
