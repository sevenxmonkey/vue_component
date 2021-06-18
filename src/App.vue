<template>
  <div id="app">
    <Tree :folder="root"/>
  </div>
</template>

<script>
import Tree from "./components/Tree.vue";

export default {
  name: "App",
  components: {
    Tree,
  },
  data() {
    return {
      root: {
        text: "Root Folder",
        leaf: false,
        expanded: true,
        children: [
          {
            text: "Sub Folder 1",
            leaf: false,
            expanded: false,
            children: [
              {
                text: "Sub Sub Folder 1",
                leaf: false,
                expanded: false,
                children: [
                  {
                    text: "SomeFile1.js",
                    leaf: true,
                  },
                ],
              },
              {
                text: "Sub Sub Folder 2",
                leaf: false,
                expanded: false,
                children: [],
              },
              {
                text: "SomeFile.txt",
                leaf: true,
              },
            ],
          },{
            text: "Sub Folder 2",
            leaf: false,
            expanded: false,
          }
        ],
      },
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
