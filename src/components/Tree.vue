<template>
  <ul class="folders">
    <folder :folder="root"></folder>
  </ul>
</template>

<script>
import Folder from "./Folder.vue";

export default {
  name: "Tree",
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
          },
          {
            text: "Sub Folder 2",
            leaf: false,
            expanded: false,
          },
        ],
      },
    };
  },
  components: {
    Folder,
  },
};
</script>

<style scoped>
ul.folders {
  padding: 1rem;
  margin: 0;
  box-sizing: border-box;
  width: 100%;
  list-style: none;
}
ul.folders > li:first-child {
  padding: 1rem 1rem 1rem 0;
}
</style>