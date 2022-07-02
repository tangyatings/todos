<template>
  <div id="app">
    <div class="todo">
      <div class="title">todos</div>
      <div class="main">
        <my-header />
        <list />
        <my-footer v-if="allTodo.length" :allTodo="allTodo"/>
      </div>
    </div>
  </div>
</template>

<script>
import {eventBus} from './main.js'

import MyHeader from './components/header.vue';
import List from './components/list.vue';
import MyFooter from './components/footer.vue'
export default {
  name: 'App',
  data(){
    return {
      allTodo:[]
    }
  },
  created(){
    eventBus.$on('get-all-todo',(allTodo)=>{
      this.allTodo = allTodo;
    })
  },
  components: {
    MyHeader,
    List,
    MyFooter
  }
}
</script>

<style lang="css">
body{
  padding: 0;
  margin: 0 auto;
  font:14px 'Helvetica Neue', Helvetica, Arial, sans-serif;
  background: #f5f5f5;
  color: #4d4d4d;
  min-width: 230px;
  max-width: 550px;
  font-weight: 300;
}
.todo{
  width: 550px;
  margin: 0 auto;
}
.title{
  font-size: 100px;
  width: 100%;
  text-align: center;
  font-weight: 100;
  color: rgba(175, 47, 47, 0.15)
}
.main{
    background: #fff;
    position: relative;
    box-shadow: 0 2px 4px 0 rgb(0 0 0 / 20%), 0 25px 50px 0 rgb(0 0 0 / 10%);
}
</style>
