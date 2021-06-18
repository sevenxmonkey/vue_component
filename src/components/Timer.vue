<template>
  <div class="container">
    <div v-if="triggerAlert" class="alert">Alert Modal</div>
    <div v-if="status === 'init'" class="input-list">
      <div class="input-item">
        <select name="hour" v-model="inputHour" @change="onInputTime">
          <option v-for="item in optionsHour" :key="item">{{item}}</option>
        </select>
        <label for="hour">Hour</label>
      </div>

      <div class="input-item">
        <select name="minute" v-model="inputMinute" @change="onInputTime">
          <option v-for="item in optionsMinute" :key="item">{{item}}</option>
        </select>
        <label for="minute">Minute(s)</label>
      </div>

      <div class="input-item">
        <select name="second" v-model="inputSecond" @change="onInputTime">
          <option v-for="item in optionsSeconds" :key="item">{{item}}</option>
        </select>
        <label for="second">Second(s)</label>
      </div>

    </div>
    <div v-else class="input-list time-num">
      {{formatHour(curTimeObj.hour)}} : 
      {{formatHour(curTimeObj.minute)}} : 
      {{formatHour(curTimeObj.second)}}
    </div>
    <div class="input-list">
      <div v-if="status === 'init'" class="input-item">
        <button @click="startProcess">Start</button>
        <button @click="resetTime">Reset</button>
      </div>

      <div v-if="status === 'process'" class="input-item">
        <button @click="resetTime">Cancel</button>
        <button @click="pauseProcess">Pause</button>
      </div>

      <div v-if="status === 'pause'" class="input-item">
        <button @click="resetTime">Cancel</button>
        <button @click="recoverProcess">Continue</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
    name:"Timer",
    data(){
      return {
        //input
        optionsHour: [],
        optionsMinute: [],
        optionsSeconds: [],

        inputHour: 0,
        inputMinute: 0,
        inputSecond: 0,

        startTime: null,
        endTime: null,
        leftTime: 0,
        totalTime: 0,

        curTimeObj:{
          hour: 0,
          minute: 0,
          second: 0
        },
        //state
        status: 'init', // 'init', 'process', 'pause'
        triggerAlert: false,
        
        intervalFunc: null,
      }
    },
    mounted(){
      this.initSelections();
    },
    methods:{
      onInputTime(){
        this.leftTime = (this.inputHour * 3600 + this.inputMinute * 60 + this.inputSecond) * 1000;
        this.formateLeftTime();
      },
      startProcess(){
        this.status = 'process';
        this.triggerAlert = false;
        this.startTime = Date.now();
        this.endTime = Date.now() + this.leftTime;
        this.intervalFunc = setInterval(this.onPassStep, 1000);
      },

      onPassStep(){
        if(Date.now() >= this.endTime){
          console.log("Alert Modal!");
          this.resetTime();
          this.status = 'init';
          this.triggerAlert = true;
        }
        this.leftTime = Math.max(this.endTime - Date.now(), 0);
        this.formateLeftTime();
      },

      formateLeftTime(){
        const ls = (this.leftTime) / 1000;
        this.curTimeObj.hour = Math.floor(ls / 3600);
        this.curTimeObj.minute = Math.floor((ls % 3600) / 60);
        this.curTimeObj.second = Math.round(ls % 60);
        console.log(this.curTimeObj.hour, this.curTimeObj.minute, this.curTimeObj.second);
      },

      resetTime(){
        this.inputHour = 0;
        this.inputMinute = 0;
        this.inputSecond = 0;

        this.startTime = null;
        this.endTime = null;

        this.leftTime = 0;
        this.totalTime = 0;

        this.status = 'init';
        this.curTimeObj = {
          hour: 0,
          minute: 0,
          second: 0,
        },
        this.triggerAlert = false;
        if(this.intervalFunc){
          clearInterval(this.intervalFunc);
        }
      },

      pauseProcess(){
        this.status = 'pause'
        if(this.intervalFunc){
          clearInterval(this.intervalFunc);
        }
      },
      recoverProcess(){
        this.endTime = this.leftTime + Date.now();
        this.startProcess()
      },
      
      initSelections(){
        for(let i = 0; i < 60; i++){
          this.optionsHour.push(i);
          this.optionsMinute.push(i);
          this.optionsSeconds.push(i);
        }
      },

      formatHour(val){
        return String(val).length === 2 ? String(val) : '0' + val;
      }
    }
}
</script>

<style scoped>
button{
  margin: 5px;
  border: none;
  padding: 10px;
  border-radius: 3px;
  cursor: pointer;
}
button:hover{
  background-color: yellow;
}
.container{
  text-align: center;
}
.input-list{
  display: flex;
  justify-content: center;
}

.input-item{
  margin: 5px;
}

.time-num{
  font-size: 24px;
  font-weight: 800;
}

.alert{
  color:red;
  font-size: 24px;
}

</style>