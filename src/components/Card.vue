<template>
    <div :class="{uncheck, correct,wrong}" id='container'>
        <span>{{error[this.id]}}</span>
        <p>{{id+1}}. {{question.question}}</p>
        <Option type="radio" :name='id' :value="question.a" v-on:choose='updateChoose($event)' :correctAnswer='correctAnswer'></Option>
        <Option type="radio" :name='id' :value="question.b" v-on:choose='updateChoose($event)' :correctAnswer='correctAnswer'></Option>
        <Option type="radio" :name='id' :value="question.c" v-on:choose='updateChoose($event)' :correctAnswer='correctAnswer'></Option>
        <Option type="radio" :name='id' :value="question.d" v-on:choose='updateChoose($event)' :correctAnswer='correctAnswer'></Option>
        <span :class="{display:uncheck}" >Unanswered</span>
        <span :class="{display:wrong}" style="color:red">Wrong</span>
        <span :class="{display:correct}" style="color:green">Correct</span>
    </div>
</template>

<script>
import Option from './Option.vue'
export default {
    props:['question','id',"error", 'correctAnswer'],
    components:{
        Option
    },
    data () {
        return {
            answer: null,
            uncheck:null,
            correct:null,
            wrong:null
        }   
    },
    methods:{
        updateChoose:function(a){
            this.$emit('answer', {index:a.index,answer:a.answer})
            console.log(this.correctAnswer);
            
        }
    },
    beforeUpdate:function(){
        if(this.error[this.id].checked == false){
            this.uncheck=true
            this.correct=false
            this.wrong=false
        }
        else if(this.error[this.id].wrong==true){
            this.wrong=true
            this.correct=false
            this.uncheck=false
        }
        else if(this.error[this.id].correct==true){
            this.correct=true
            this.wrong=false
            this.uncheck=false
            }

        
        
        
    }
}
</script>
<style scoped>
p{
    margin-bottom: 10px;
}


label{
    margin: 5px;
    
}
#container{
    padding: 20px;
    
    border: 2px solid rgba(128, 128, 128, 0.534);
    border-radius: 5px;
    margin: auto;
    margin-bottom: 10px;
    width:65%;
}
    .wrong{
        border: 3px solid red;
    }
    .uncheck{
        border: 3px solid rgb(218, 218, 27);
    }
    .correct{
        border: 3px solid lightgreen;
    }
    span{
        display:none;
        float:right;
    }
    
    .display{
        display:inline-block;
    }
    
@media only screen and (max-width: 1030px) {
    div{
        width: 85%;
    }
}

@media only screen and (max-width: 400px) {
    div{
        width: 300px;
        
        
        
    }
}

</style>