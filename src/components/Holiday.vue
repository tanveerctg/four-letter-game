<template>
  <q-page class="q-py-lg q-gutter-y-md">
   <div class="text-h4 text-center">Holiday Calendar {{year}}</div>

      <div v-for="(month,index) in months" :key="index" style="max-width:1100px;width:100%;margin:0 auto;" class="flex justify-between items-center q-gutter-y-lg">
          <span class="text-h6">{{month.name}}</span>
          <div class="flex items-center q-gutter-x-md">
            <div class="flex q-gutter-x-lg">  
              <div v-for="(holiday,index) in month.holidays" :key="index" style="border-bottom:2px solid blue;cursor:pointer;" class="text-h6">
                <span v-if="holiday.date">{{holiday.date}}</span>
                <span v-else>{{holiday.startDate}} - {{holiday.endDate}}</span>
                <q-tooltip anchor="top middle" self="bottom middle" :offset="[10, 10]">
                 <span class="text-body2">{{holiday.reason}}</span>
                </q-tooltip>            
              </div>
            </div>
            <q-btn round color="primary" icon="add" size="xs" @click="addHoliday(index,year)"/>
          </div>
      </div>
      <Form :prompt="prompt" :daysInMonth="daysInMonth" :month="month" @promptClose="promptCloseHandler" @submit="submit"/>
  </q-page>
</template>

<script>
import { date } from 'quasar'
import Form from './Form'

export default {
  name:"Holiday",
  components:{
    Form
  },
  data(){
    return{
      year:null,
      months:[
      {name:'January',holidays:[]},
      {name:'February',holidays:[]},
      {name:'March',holidays:[]},
      {name:'April',holidays:[]},
      {name:'May',holidays:[]},
      {name:'June',holidays:[]},
      {name:'July',holidays:[]},
      {name:'August',holidays:[]},
      {name:'September',holidays:[]},
      {name:'October',holidays:[]},
      {name:'November',holidays:[]},
      {name:'Decmber',holidays:[]}
      ],
      prompt: false,
      daysInMonth:null,
      month:null
    }
  },
  mounted(){
    let timeStamp = Date.now()
    let getYear = date.formatDate(timeStamp, 'YYYY')
    this.year=getYear
  },
  methods:{
    addHoliday(month,year){  
      const daysInMonth=new Date(year, month+1, 0).getDate();
      this.daysInMonth=daysInMonth; 
      this.month=this.months[month].name
      this.prompt=true
    },
    cancelHandler(){
      this.date=null;
      this.startDate=null;
      this.endDate=null;
      this.type=null;
    },
    onSubmit(){
      console.log('ok')
    },
    promptCloseHandler(){
       this.prompt = false
    },
    submit(data){
      const {month,startDate,endDate,reason}=data;
      this.months.find(m=>{
        if(m.name==month){
          m.holidays.push(data)
        }
      })
      this.prompt = false
    }
  }
}
</script>
