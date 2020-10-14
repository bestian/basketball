<template>
  <div id="app">
    <aplayer autoplay mini :repeat="'repeat-one'"
    :music="{
      title: 'Background',
      artist: 'Game',
      src: 'https://bestian.github.io/basketball/happy.mp3'
    }"
    />
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

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
