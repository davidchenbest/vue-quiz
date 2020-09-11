<template>
  <div >
    <template v-for="(q,index) in questions" >
      <div :class='{correct:answer[index],wrong:wrong[index]}' :key='index'>
         
        <card  :question="q" :id='index' v-on:answer='updateAnswer($event)' :checklist='result'></card>
        <!-- <p :class='{display:!wrong[index]}'>Wrong{{wrong[index]}}</p> -->
      </div>
    </template>
    <button  @click="submit">Submit</button>
    <p>{{error}}</p>
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
      this.answer.forEach((item,i)=>{
        if(item === null) this.unanswered.push(i);        
        else if(item == this.questions[i].answer ){
          this.result[i] =true
        }
        else  this.result[i] =false
      })
      if(this.unanswered.length > 0) {
        this.error = 'not finished'
        this.unanswered=[]
      }
      else {
        this.error=''
        //console.log(this.result);
        }
      
      this.result=[...this.result]
    },
    updateAnswer:function(a){
      
      if(this.questions[a.index].answer == a.answer){
        this.answer[a.index]=true
      }
      else this.answer[a.index]=false
      console.log(this.answer);
    }
  },
  data:function(){
    return{
      questions:[
        {question:'what is 5+5?', a:1, b:2, c:3, d:10, answer:10 },
        {question:'what is 5+6?', a:1, b:2, c:3, d:11, answer:11 }
      ],
      answer:[],
      unanswered:[],
      result:[],
      wrong:[],
      error:'',
      
      
    }
  },
  mounted:function(){
    for(let i=0; i< this.questions.length; i++){
      this.answer[i]=null;
      this.wrong[i]=null;
    }
  }
}
</script>

<style>
  .correct{
    border: 3px solid green;
  }
  .wrong{
    background-color: red;
  }
  .display{
    display:none;
  }
</style>
