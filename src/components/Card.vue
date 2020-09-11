<template>
    <div :class="{uncheck, correct,wrong}">
        <span>{{error[this.id]}}</span>
        <p>{{id+1}}. {{question.question}}</p>
        <input type="radio" :name='id' :value="question.a" @click="choose"><label>{{question.a}}</label><br>
        <input type="radio" :name='id' :value="question.b" @click="choose"><label>{{question.b}}</label><br>
        <input type="radio" :name='id' :value="question.c" @click="choose"><label>{{question.c}}</label><br>
        <input type="radio" :name='id' :value="question.d" @click="choose"><label>{{question.d}}</label>
        <span :class="{display:uncheck}" >Unanswered</span>
        <span :class="{display:wrong}" style="color:red">Wrong</span>
        <span :class="{display:correct}" style="color:green">Correct</span>
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
p{
    margin-bottom: 10px;
}

input{
    margin-left: 30px;
    
}
label{
    margin: 5px;
    
}
div{
    padding: 20px;
    
    border: 2px solid rgba(128, 128, 128, 0.534);
    border-radius: 5px;
    margin: auto;
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