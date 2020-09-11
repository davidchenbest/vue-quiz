<template>
    <div>
        <p>{{id+1}}. {{question.question}}</p>
        <input type="radio" :name='id' :value="question.a" @click="choose"><label>{{question.a}}</label><br>
        <input type="radio" :name='id' :value="question.b" @click="choose"><label>{{question.b}}</label><br>
        <input type="radio" :name='id' :value="question.c" @click="choose"><label>{{question.c}}</label><br>
        <input type="radio" :name='id' :value="question.d" @click="choose"><label>{{question.d}}</label>
    </div>
</template>

<script>
export default {
    props:['question','id'],
    data () {
        return {
            answer: null,
        }
    },
    methods:{
        choose:function(e){
            this.answer = e.target.value
            this.$emit('answer', {index:e.toElement.name,answer:this.answer})
        }
    },
    mounted:function(){
        
    }
}
</script>
<style scoped>
    
    
    
</style>