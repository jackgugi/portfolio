<template>
  <div id="app">
    <Layout />
  </div>
</template>

<script>
import Layout from './components/Layout.vue'

export default {
  name: 'App',
  components: {
    Layout
  }
}
</script>

<style>
@font-face {
    font-family: 'ultraregular';
    src: url('./assets/fonts/ultra-webfont.woff2') format('woff2'),
         url('./assets/fonts/ultra-webfont.woff') format('woff'),
         url('./assets/fonts/Ultra.otf') format('otf');
    font-weight: normal;
    font-style: normal;
}

body {
    background: #000000;
    margin: 0;
    min-height: 100vh;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
