<template>
  <div >
    <template v-for="(q,index) in questions" >
      
         
      <card :key='index' :question="q" :id='index' v-on:answer='updateAnswer($event)' :error='error' ></card>
        
    </template>
    <button  @click="submit">Submit</button>
    <p>{{msg}}</p>
  </div>
</template>

<script>
import Card from './components/Card.vue'

export default {
  components: {
    card:Card
  },
  methods:{
    submit:function(){
      this.msg=''
      this.error.forEach((item)=>{
        if(item.checked ==false) {this.msg = 'unfinshed'}
      })
        this.error=[...this.error]
      
      if(this.msg.length==0){
        this.error.forEach((item,index)=>{
          if(this.answer[index]==false) item.wrong=true
          else if(this.answer[index]==true) item.correct=true
        })
      }
      
    },
    updateAnswer:function(a){
      this.error[a.index].checked=true;
      if(this.questions[a.index].answer == a.answer){
        this.answer[a.index]=true
      }
      else this.answer[a.index]=false
      
    }
  },
  data:function(){
    return{
      questions:[
        {question:'what is 5+5?', a:1, b:2, c:3, d:10, answer:10 },
        {question:'what is 5+6?', a:1, b:2, c:3, d:11, answer:11 }
        
      ],
      answer:[],
      error:[],
      msg:'',
      

    }
  },
  mounted:function(){
    for(let i=0; i< this.questions.length; i++){
      this.answer[i]=null
      this.error[i] = { wrong:null, checked:false, correct:null}
    }
    
  }
}
</script>

<style>
  
</style>
