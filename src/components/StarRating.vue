<template>
  <div class="container">
      <!-- Stars -->
      <div class="stars-list">
            <div class="icon-star" 
                v-for="(score, index) in stars" :key="index"
                :class="score <= rate ? 'hightlight' : ''"
                @click="onClickScore(score)"></div>
      </div>
      <div class="text">{{rate}}</div>
  </div>
</template>

<script>
export default {
    name: "StarRating",
    props:{
        initialRate: Number
    },
    data(){
        return {
            stars: [1, 2, 3, 4, 5],
            rate: 0,
        }
    },
    mounted(){
        this.rate = this.initialRate;
    },
    methods:{
        onClickScore(score){
            this.rate = score;
            this.$emit('onConformScore', this.rate);
        }
    }
}
</script>

<style scoped>
.container{
    display: flex;
    justify-content: center;
    align-items: center;
}
.text{
    text-align: center;
    font-size: 18px;
    margin: 5px;
}
.stars-list{
    display: flex;
    justify-content: center;
}
.icon-star{
    width: 30px;
    height: 30px;
    margin: 5px;
    border-radius: 100px;
    box-shadow: inset 0 0 5px #0000005e;
    cursor: pointer;
}

.hightlight{
    background-color: rgb(255, 196, 0);
}
</style>