<template>
	<div class="flex-row justify-center">
	 <div class="flex q-gutter-sm"> 
	 	<div style="width:50px;height:50px;border-radius:50%;border:1px solid grey;">S</div>
	 	<div style="width:50px;height:50px;border-radius:50%;border:1px solid grey;"></div>
	 	<div style="width:50px;height:50px;border-radius:50%;border:1px solid grey;"></div>
	 	<div style="width:50px;height:50px;border-radius:50%;border:1px solid grey;"></div>
	 </div>
	 <div style="width:150px;position:relative;background:red;height:100px;" >


	 	<div style="position:absolute;width:40px;height:40px;border-radius:50%;background:blue;display:flex;justify-content:center;align-items:center;color:white;font-size:1.5rem;" 
	 	v-for="(ltr,index) in current"
	 	v-bind:class="{ active_0: index==0,active_1: index==1,active_2: index==2,active_3: index==3}"
	 	@click="clickAlphabet(ltr)"
	 	>{{ltr.letter}}</div>
	 </div>
	 {{insertedLetters}}
	</div>
</template>

<script>

export default {
  name:"index",
  data(){
  	return{
  		words:['dale','lion','tale','mars','rail'],
  		current:null,
  		clicked:false,
  		insertedLetters:[]
  	}
  },
  mounted(){
  	const c_word=this.words[2].split('').map((l,index)=>{ return {letter:l,index,clicked:false}});
  	console.log(c_word)
  	this.current=c_word;
  },
  components:{
  },
  methods:{
  	clickAlphabet(info){


  		if(!info.clicked){
  			this.current.splice(info.index,1,{...info,clicked:true})
  			this.insertedLetters=[...this.insertedLetters,info]
  		}else{
  			this.current.splice(info.index,1,{...info,clicked:false})
  			
  			const findIndexNumber=this.insertedLetters.findIndex(letter=>letter.index==info.index);
  			console.log(findIndexNumber)

  			this.insertedLetters.splice(findIndexNumber,1)
  			
  		}

  	
  	}
  }
}
</script>
<style>
	.active_0{
		top:50%;transform:translateY(-50%);
	}
	.active_1{
		left:50%;bottom:0;transform:translateX(-50%);
	}
	.active_2{
		right:0;top:50%;transform:translateY(-50%);
	}
	.active_3{
		left:50%;transform:translateX(-50%);
	}
</style>
