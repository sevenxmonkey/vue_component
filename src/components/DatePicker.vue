<template>
  <div class="container">
      <div class="card">
        <div class="display-date">{{year}} - {{monthDict[month]}} - {{day}}</div>
        <div class="select-list">
            <div class="selection year">
                <label for="year">Year</label>
                <select name="year" v-model="year" @change="onChangeSelect">
                    <option v-for="item in yearSelection" :key="item">{{item}}</option>
                </select>
            </div>
            <div class="selection month">
                <label for="month">Month</label>
                <select name="month" v-model="month" @change="onChangeSelect">
                    <option v-for="item in monthSeleciotn" :key="item" :value="item">{{monthDict[item]}}</option>
                </select>
            </div>
        </div>
        <div class="calendar-container">
            <div class="c-row">
                <div class="c-item calendar" v-for="(item, index) of weekDict" :key="index">{{item}}</div>
            </div>
            <div class="c-row" v-for="(line, id1) of dayLayout" :key="id1">
                <div class="c-item calendar date" 
                    v-for="(item, id2) of line" :key="id2"
                    :class="dateStyleController(dayLayout[id1][id2])"
                    @click="onClickDate(dayLayout[id1][id2])">
                    {{dayLayout[id1][id2]}}
                </div>
            </div>
        </div>
        <div class="btns">
            <button>Cancel</button>
            <button @click="onConfirm">Confirm</button>
        </div>
      </div>
  </div>
</template>

<script>
export default {
    name: "DatePicker",
    data(){
        return {
            yearSelection: [],
            monthSeleciotn: [],
            daySelection: [],

            year: 0,
            month: 0,
            day: 0,

            weekdayOfFirstDay: null,
            numofWeeks: null,
            dayLayout: [],

            weekDict:['S', 'M', 'T', 'W', 'T', 'F', 'S'],
            monthDict: ['Jan', 'Feb', 'Mar', 'Apr', 'May', 'Jun', 'Jul', 'Aug', 'Sep', 'Oct', 'Nov', 'Dec'],
        }
    },
    mounted(){
        const curDate = new Date();
        this.year = curDate.getFullYear();
        this.month = curDate.getMonth();
        this.day = curDate.getDate();
        this.genYearSeleciton(curDate);
        this.genMonthSelection(curDate);
        this.genWeekLauout(curDate);
    },
    methods:{
        genYearSeleciton(){
            this.yearSelection = [];
            for(let i = 0; i < 10; i++){
                this.yearSelection.push(this.year - 5 + i);
            }
            this.yearSelection.sort((a,b) => b - a);
        },
        genMonthSelection(){
            this.monthSeleciotn = [];
            for(let i = 0; i < 12; i ++){
                this.monthSeleciotn.push(i);
            }
        },
        //Event Controller
        onChangeSelect(){
            this.genWeekLauout(new Date(this.year, this.month, this.day));
        },
        onClickDate(day){
            if(day){
                this.day = day;
            }
        },
        onConfirm(){
            const selectDate = new Date(this.year, this.month, this.day);
            this.$emit('onConfirmDate', selectDate);
        },
        //helperfunction
        genWeekLauout(date){
            //offSetToFirstDay
            const year = date.getFullYear();
            const month = date.getMonth();
            const lo = new Date(year, month, 1);
            const hi = new Date(year, month + 1, 0)
            
            //calculate layout
            const m = Math.ceil((lo.getDay() + hi.getDate()) / 7)
            const matrix = [];
            for(let i = 0; i < m; i++){
                const arr = [];
                for(let j = 0; j < 7; j++){
                    const cnt = i * 7 + j - lo.getDay() + 1;
                    if(cnt < 1 || cnt > hi.getDate()){
                        arr.push('');
                    }else{
                        arr.push(String(cnt));
                    }
                }
                matrix.push(arr);
            }
            this.dayLayout = matrix;
        },
        dateStyleController(day){
            if(!day){
                return 'blankdate';
            }else if(day == this.day){
                return 'selecteddate';
            }
        }
    }
}
</script>

<style scoped>
.container{
    height: 100vh;
    width: 100vw;
    position: relative;
}
.card{
    width: 300px;
    height: 380px;
    background-color: white;
    box-shadow: 3px 3px 6px rgba(0, 0, 0, 0.1);
    padding: 10px;

    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
}
.display-date{
    margin: 10px;
    font-size: 18px;
    font-weight: 800;
    text-align: center;
}
label{
    margin: 0 5px;
}
.select-list{
    display: flex;
    justify-content: center;
}
.c-row{
    display: flex;
    justify-content: center;
}
.calendar{
    width: 25px;
    height: 25px;
    text-align: center;
    padding: 3px;
    margin: 3px;
    font-size: 12px;
}

.date{
    background-color: rgba(0, 0, 0, 0.1);
    border-radius: 50px;
    cursor: pointer;
}

.selecteddate{
    background-color: black;
    color: white;
}

.blankdate{
    opacity: 0.5;
}

.btns{
    position: absolute;
    bottom: 20px;
    right: 27px;
}
.btns button{
    border: none;
    padding: 10px;
    border-radius: 5px;
    margin: 5px;
    cursor: pointer;
}
.btns button:hover{
    background-color: rgba(255, 188, 5, 0.418);
}
</style>