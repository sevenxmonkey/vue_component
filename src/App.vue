<template>
  <div id="app">
    <StarRating :initialRate="2"/>
  </div>
</template>

<script>
import StarRating from './components/StarRating.vue'

export default {
  name: 'App',
  components: {
    StarRating
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
