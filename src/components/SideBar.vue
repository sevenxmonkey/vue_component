<template>
  <div class="sidebar">
      <div class="sidebar-backdrop"
        @click="closeSidebarPanel" v-if="isPanelOpen"></div>
    <transition name="slide">
        <div name="slide">
            <div v-if="isPanelOpen" class="sidebar-panel">
                <slot></slot>
            </div>
        </div>
    </transition>
  </div>
</template>

<script>
export default {
    data(){
        return {
            isPanelOpen: true,
        }
    },
    methods: {
        closeSidebarPanel(){
            this.isPanelOpen = false
        }
    }
}
</script>

<style>

</style>