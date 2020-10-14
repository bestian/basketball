<template>
  <div id="app">
    <nav>
      <aplayer autoplay mini :repeat="'repeat-one'"
      :music="{
        title: 'Background',
        artist: 'Game',
        src: 'https://bestian.github.io/basketball/happy.mp3'
      }"
      />
      <span>點擊籃球或按空白鍵</span>
    </nav>
    <router-view/>
  </div>
</template>

<script>
import Aplayer from 'vue-aplayer'

export default {
  name: 'App',
  components: {
    Aplayer
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  position: relative;
  z-index: 999;
}

</style>
