<template>
  <div >
    <div id='header'>Quiz Application</div>
    <div v-if='score' style="text-align: center;">
      <p style="text-decoration: underline;">Results</p>
      <p>You got {{score*questions.length/100}} / {{questions.length}} questions correct</p>
      <p>{{score}}%</p>
    </div>
    <template v-for="(q,index) in questions" >
      
         
      <card :key='index' :question="q" :id='index' v-on:answer='updateAnswer($event)' :error='error' ></card>
        
    </template>
    <button id='center'  @click="submit">Submit</button>
    <p id='msg'>{{msg}}</p>
  </div>
</template>

<script>
import Card from './components/Card.vue'
const data = require('./questions.json');
export default {
  components: {
    card:Card
  },
  methods:{
    submit:function(){
      this.msg=''
      this.error.forEach((item)=>{
        if(item.checked ==false) {this.msg = 'Answer all before submitting'}
      })
        this.error=[...this.error]
      
      if(this.msg.length==0){
        this.error.forEach((item,index)=>{
          if(this.answer[index]==false) item.wrong=true
          else if(this.answer[index]==true) item.correct=true
          this.getScore()
        })
      }
      
    },
    getScore:function(){
      let correct =0;
      this.answer.forEach((item)=>{
        if(item == true){
          correct++;
        }
      })
      this.score=100* correct/ this.answer.length
     
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
      questions:data,
      answer:[],
      error:[],
      msg:'',
      score:0
      

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

<style scoped>

#header{
  background-color: rgb(153, 10, 10);
  width: 100%;
  padding: 10px;
  margin-bottom: 20px;
  color: white;
  
}
div{
  
  margin-bottom: 10px;
  
}
button{
  background-color: green;
  color:white;
  width: 65px;
  height: 25px;
  margin: 10px 0;
  position: absolute;
  left: 50%;
  -ms-transform: translate(-50%, -50%);
  transform: translate(-50%, -50%);
}
#msg{
  text-align: center;
  margin: 10px 0;
  position: relative;
  top:35px;
  color: red;
  font-weight: bold;
  
}
  
</style>
