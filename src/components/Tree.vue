<template>
  <ul class="folders">
    <folder :folder="folder"></folder>
  </ul>
</template>

<script>
import Folder from './Folder.vue';

export default {
  name: 'Tree',
  props: {
    folder: Object
  },
  components: {
    Folder
  }
};
</script>

<style scoped>
ul.folders {
  padding: 1rem;
  margin: 0;
  box-sizing: border-box;
  width: 100%;
  list-style: none
}
ul.folders > li:first-child {
  padding: 1rem 1rem 1rem 0
}
</style>