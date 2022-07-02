<template>
  <div class="footer">
    <div class="left-todo">{{allTodo.length}} items left</div>
    <div class="filter-todo">
      <button class="all" @click="showAll">all</button>
      <button class="active" @click="showActive">active</button>
      <button class="completed" @click="showCompleted">completed</button>
    </div>
    <div v-if="ifCompleted" class="clear-all-todo" @click="clearAllTodo">clear completed</div>
  </div>
</template>

<script>
import {eventBus} from '../main'
export default {
    name:'el-footer',
    props:['allTodo'],
    computed:{
      ifCompleted(){
        return this.allTodo.indexOf(item=>{
          return item.checked;
        })
      }
    },
    methods:{
      showAll(){
        eventBus.$emit('updateAllTodoCopy',this.allTodo)
      },
      showActive(){
        const active = this.allTodo.filter(item=>{
            return !item.checked
        })
        eventBus.$emit('updateAllTodoCopy',active)
      },
      showCompleted(){
        const completed = this.allTodo.filter(item=>{
            return item.checked
          })
        eventBus.$emit('updateAllTodoCopy',completed)
      },
      clearAllTodo(){
        const completed = this.allTodo.filter(item=>{
            return !item.checked
          })
        eventBus.$emit('clearAllTodo',completed)
      }
    }
}
</script>

<style>
.footer{
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0px 20px;
}
.filter-todo button{
  background-color: white;
  margin: 5px ;
  box-sizing: border-box;
  border: 1px solid rgba(0, 0, 0,0);

}
.filter-todo button:hover{
  box-sizing: border-box;
  
  border: 1px solid pink;
  opacity: .4;
}
.clear-all-todo:hover{
  border-bottom: lightgray;
}
</style>