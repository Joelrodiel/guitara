<template>
  <div id="app">
    <Chord/>
  </div>
</template>

<script>
import Chord from './components/Chord'

export default {
  name: 'App',
  components: {
    Chord
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
body {
  background-color: #ECF0F1;
}
</style>
