<template>
  <li class="folder" :class="[folder.leaf ? 'is-leaf' : 'is-folder']">
    <div><span @click="expand">{{ folder.text }}</span></div>
    <ul
      class="sub-folders"
      v-if="folder.children && folder.children.length > 0"
      v-show="folder.expanded"
    >
      <folder
        v-for="(child, index) in folder.children"
        :key="index"
        :folder="child"
      ></folder>
    </ul>
    <div class="folder-empty" v-else v-show="!folder.leaf && folder.expanded">
      No Data
    </div>
  </li>
</template>

<script>
export default {
  name: "folder",
  props: {
    folder: Object,
  },
  methods: {
    expand() {
      if (this.folder.leaf) {
        return;
      }
      this.folder.expanded = !this.folder.expanded;
    },
  },
};
</script>

<style scoped>
li.is-folder {
  padding-left: 1rem;
  
}
li.is-folder span {
  padding: 0.5rem 0;
  cursor: pointer;
  font-weight: 800;
}
li.is-leaf {
  padding: 0 0 0 1rem;
  color: rgba(0, 0, 0, 0.5);
}
ul.sub-folders {
    border-left: 1px solid #d3d3d3;
  padding: 0 1rem 0 0;
  margin: 0;
  box-sizing: border-box;
  width: 100%;
  list-style: none;
}
div.folder-empty {
    border-left: 1px solid #d3d3d3;
  padding: 0 1rem 0 1rem;
  color: rgba(0, 0, 0, 0.5);
}
</style>