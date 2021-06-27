<template>
  <div class="container">
      <h1>CSS Transition</h1>
      <ul>
          <li>The CSS property you want to add an effect to.</li>
          <li>The duration of the effect.</li>
      </ul>
      <!-- Demo1 -->
      <div id="demo1"></div>
      <!-- Demo2 -->
      <button @click="showSideBar = !showSideBar">
          Toggle
      </button>
      <transition name="fade">
          <div class="sidebar" v-if="showSideBar">hello</div>
      </transition>

  </div>
</template>

<script>
export default {
    name: "CSSTransition",
    data(){
        return {
            showSideBar: false,
        }
    }
}
</script>

<style scoped>
.container{
    margin: 50px;
    position: relative;
}
#demo1{
    cursor: pointer;
    width: 50px;
    height: 50px;
    background-color: black;
    transition: width 1s ease-out, background-color 0.5s ease-out;
}

#demo1:hover{
    width: 100px;
    background-color: rgb(255, 187, 0);
}

.fade-enter-active, .fade-leave-active{
    transition: transform .5s;
}

.fade-enter, .fade-leave-to{
    transform: translateX(100%)
}

.sidebar{
    position: fixed;
    top: 0;
    right: 0;
    height: 100%;
    width: 300px;
    background-color: white;
    box-shadow: -2px -1px 3px rgba(0, 0, 0, 0.2);
}
</style>