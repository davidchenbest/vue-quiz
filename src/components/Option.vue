<template>
    <div>
        <span>
        <input type="radio" :name='name' :value="value" @click="choose"><label :class="{correct:highlight}">{{value}}</label><br>
        </span>
        
        
        
    </div>
</template>
<script>
export default {
    props:['name','value', 'correctAnswer'],
    data() {
        return {
            show: this.correctAnswer.showAnswer,
            answer: this.correctAnswer.correctAnswer
        }
    },
    methods: {
        choose:function(e){
            this.$emit('choose', {index:e.toElement.name,answer:e.target.value})
            
        }
    },
    computed:{
        highlight:function(){
            if(this.show && this.answer === this.value){
                console.log(true);
                return true
            }
            return false
        }
    }
}
</script>
<style scoped>
    input{
    margin-left: 30px;
    margin-right:5px;
    
}
span{
    display:flex;
    align-items: center;
}
.correct{
    background-color: lightgreen;
    flex-grow: 2;
}
</style>