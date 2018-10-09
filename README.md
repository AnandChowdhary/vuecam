# vue-html5-camera

Add `vue-html5-camera` to your Vue.js project:

```bash
yarn add -html5-camera
```

Then use it:

```html
<template>
  <main>
    <Camera ref="camera" width="300" height="300" />
    <button @click="getPhoto">Click photo</button>
    <img alt="Your image" :src="src" v-if="src">
  </main>
</template>
```
```js
import Camera from "vue-html5-camera"
export default {
  data() {
    return {
      src: ""
    }
  },
  methods: {
    getPhoto() {
      this.src = this.$refs.camera.click();
    }
  },
  components: {
    Camera
  }
}
```

## Development

Clone this repository and install dependencies:

```
yarn
```

### Compiles and hot-reloads for development
```
yarn serve
```

### Compiles and minifies for production
```
yarn build
```

### Lints and fixes files
```
yarn lint
```
