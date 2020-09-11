<template>
    <div :class="{uncheck, correct,wrong}">
        <span>{{error[this.id]}}</span>
        <p>{{id+1}}. {{question.question}}</p>
        <input type="radio" :name='id' :value="question.a" @click="choose"><label>{{question.a}}</label><br>
        <input type="radio" :name='id' :value="question.b" @click="choose"><label>{{question.b}}</label><br>
        <input type="radio" :name='id' :value="question.c" @click="choose"><label>{{question.c}}</label><br>
        <input type="radio" :name='id' :value="question.d" @click="choose"><label>{{question.d}}</label>
        <span :class="{display:uncheck}">Unanswered</span>
        <span :class="{display:wrong}">Wrong</span>
        <span :class="{display:correct}">Correct</span>
    </div>
</template>

<script>
export default {
    props:['question','id',"error"],
    data () {
        return {
            answer: null,
            uncheck:null,
            correct:null,
            wrong:null
        }   
    },
    methods:{
        choose:function(e){
            this.answer = e.target.value
            this.$emit('answer', {index:e.toElement.name,answer:this.answer})

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
div{
    margin:10px;
    padding:10px;
    border: 1px solid black;
}
    .uncheck, .wrong{
        border: 3px solid red;
    }
    .correct{
        border: 3px solid green;
    }
    span{
        display:none;
        float:right;
    }
    
    .display{
        display:inline-block;
    }
    
    
</style>