<template>
<div>
      <q-dialog v-model="prompt" persistent>
        <q-card style="min-width: 350px" class="q-py-md q-px-sm">
         <q-card-section class="q-pt-none">   
             <div class="text-h6">Holidays In {{month}}</div>
           </q-card-section>


        <q-form
          @submit="onSubmit"
        >

          <q-card-section class="q-pt-none q-gutter-x-md">      
              <q-radio size="xs" v-model="type" val="single" label="Single Day" />
              <q-radio size="xs" v-model="type" val="range" label="Range" />
          </q-card-section>
          <q-card-section class="q-pt-none" v-if="type=='single'">
            <q-input         
              v-model="date"
              type="number"
              label="Date"
              filled
              :rules="[ val => val && val.length > 0 || 'This field cant be empty',
              val => val > 0 && val <= daysInMonth || 'Please enter a correct Date'
              ]"
            />
          </q-card-section>
          <q-card-section class="q-pt-none flex items-center q-gutter-x-md" v-if="type=='range'">
            <q-input
              v-model="startDate"
              type="number"
              label="Start Date"
              filled
              :rules="[ val => val && val.length > 0 || 'This field cant be empty',
              val => val > 0 && val <= daysInMonth || 'Please enter a correct Date'
              ]"
            />
         
            <q-input
              v-model="endDate"
              type="number"
              label="End Date"
              filled
              :rules="[ val => val && val.length > 0 || 'This field cant be empty',
              val => val > 0 && val <= daysInMonth || 'Please enter a correct Date'
              ]"
            />
          </q-card-section>          
          <q-card-section class="q-pt-none" v-if="!!type">
            <q-input filled v-model="reason" label="Reason" :rules="[ val => val && val.length > 0 || 'Please type something']"/>
          </q-card-section>

          <q-card-section class="q-pt-none q-gutter-x-sm" v-if="!!type">
            <q-btn label="Add" type="submit" class="bg-primary text-white"/>
            <q-btn flat label="Cancel" @click="cancelHandler" class="text-red"/>
          </q-card-section>
      </q-form>
        </q-card>
      </q-dialog>
</div>

</template>

<script>

export default {
  name: 'Form',
  props:['prompt','daysInMonth','month'],
  data(){
    return{
      reason:'',
      date: '',
      startDate:null,
      endDate:null,
      type: null
    }
  },
  created(){

  },
  methods:{
    cancelHandler(){
      this.reason='';
      this.date=null;
      this.startDate=null;
      this.endDate=null;
      this.type=null;
      this.$emit('promptClose')
    },
    onSubmit(){
      this.$emit('submit',{date:this.date,startDate:this.startDate,endDate:this.endDate,month:this.month,reason:this.reason})
      this.reason='';
      this.date=null;
      this.startDate=null;
      this.endDate=null;
      this.type=null;
    }
  }
 
}
</script>
