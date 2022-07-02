<template>
  <div class="list">
    <ul>
      <li v-for="todo in allTodoCopy" :key="todo.id" :class="{'del-line':todo.checked}"> 
        <input type="checkbox" :checked="todo.checked" @change="changeChecked(todo)">
        {{todo.value}}
        <button class="delete" @click="deleteLi(todo.id)">x</button>
        </li>
    </ul>
  </div>
</template>

<script>
import {eventBus} from '../main.js'
export default {
    name:'el-list',
    data(){
      return{
        allTodo:[],
        allTodoCopy:[],
      }
    },
    created(){
      eventBus.$on('new-todo',(todo)=>{
        this.allTodo.push(todo)
        eventBus.$emit('get-all-todo',this.allTodo)
      })
      eventBus.$on('updateAllTodoCopy',(todo)=>{
        console.log(todo)
        this.allTodoCopy = todo
      })
      eventBus.$on('clearAllTodo',(todo)=>{
        this.allTodo=todo
      })
    },
    watch:{
      allTodo:function(newAllTodo){
        this.allTodoCopy = newAllTodo
      }
    },
    methods:{
      changeChecked(todo){
        this.allTodo.forEach(item=>{
          if(item.id === todo.id){
            item.checked = !item.checked
          }
        })
      },
      deleteLi(id){
        this.allTodo = this.allTodo.filter(item=>{
          return item.id!=id;
        })
        eventBus.$emit('get-all-todo',this.allTodo)
      }
    }
}
</script>

<style>
ul{
  padding: 0;
  margin: 0;
}
ul>li{
  position: relative;
  list-style: none;
  width: 100%;
  border: none;
  outline: none;
  font-size: 24px;
  font-weight: 100;
  padding: 15px 15px 15px 60px;
  border-bottom: 1px solid rgba(0, 0, 0, .1);
  box-sizing: border-box;
}
input[type='checkbox']{
  display: inline-block;
  position: absolute;
  width: 30px;
  height: 30px;
  left: 10px;
  top: 50%;
  border: none;
  margin: 0;
  padding: 0;
  border-radius: 15px;
  transform: translateY(-50%);
  background-color: white;
}
li>input[type='checkbox']:checked{
  background-color: white;
  content:'/2713'
}
.delete{
  display: none;
  width: 30px;
  height: 30px;
  position: absolute;
  right: 10px;
  top: 50%;
  transform: translateY(-50%);
  color: aqua;
  border: none;
  background-color: white;
  font-size: 24px;
  font-weight: 100;
}
ul>li:hover .delete{
  display: block;
  color: blueviolet;
}
.delete:hover .delete{
  color: tomato;
}
.del-line{
  text-decoration: line-through;
  color: rgb(0, 0, 0,.2);
}
</style>