<template>
  <div id="app">
    <div class="tabs">
      <button v-for="tab in tabs" :key="tab" @click="targetTab = tab">
        {{ tab }}
      </button>
    </div>
    <component :is="targetTab"></component>
  </div>
</template>

<script>
import DatePicker from "./components/DatePicker.vue";
import StarRating from "./components/StarRating.vue";
import Timer from "./components/Timer.vue";
import Tree from "./components/Tree.vue";
import CSSTransition from "./components/CSSTransition.vue";
import UnitConverter from "./components/UnitConverter.vue";

export default {
  name: "App",
  components: {
    DatePicker,
    StarRating,
    Timer,
    Tree,
    CSSTransition,
    UnitConverter,
  },
  data() {
    return {
      tabs: [
        "DatePicker",
        "StarRating",
        "Timer",
        "Tree",
        "CSSTransition",
        "UnitConverter",
      ],
      targetTab: "CSSTransition",
    };
  },
};
</script>

<style>
* {
  margin: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
