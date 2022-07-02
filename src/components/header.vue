<template>
  <div class="header">
    <input class="input" type="text" placeholder="What needs to be done?"  v-model="value" @keyup.enter="emitValue">
  </div>
</template>

<script>
import {eventBus} from '../main.js' 
import {nanoid} from 'nanoid'
export default {
    name:'el-header',
    data(){
      return{
        value:''
      }
    },
    methods:{
      emitValue(){
        if(this.value.trim().length>0){
          eventBus.$emit('new-todo',{id:nanoid(),value:this.value,checked:false});
          this.value=''
        }
      }
    }
}
</script>

<style scoped>
.header{
  border: none;
}
.input{
  width: 100%;
  border: none;
  outline: none;
  font-size: 24px;
  font-weight: 100;
  padding: 18px 16px 16px 60px;
  box-sizing: border-box;
}
input::before{
  content: '11';
}
</style>