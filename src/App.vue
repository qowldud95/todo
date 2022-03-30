<template>
  <div id="app">
    <div class="container">
      <div class="col-md-6 offset-md-3">
        <h1 class="text-center mb-4">Todo 어플리케이션</h1>
        <input type="text" class="form-control mb-4" v-model="userInput" @keyup.enter="addNewTodo">
        
        <div class="list-group"  v-for="(todo,index) in activeTodoList" :key="index">
          <Todo :label="todo.label" @componentClick="toggleTodoState(todo)"/>
        </div>
        
        <div class="text-right">
          <button type="button" class="btn btn-sm" @click="changeCurrentState(false)">할 일</button>
          <button type="button" class="btn btn-sm" @click="changeCurrentState(true)">완료</button>
          <button type="button" class="btn btn-sm" @click="changeCurrentState('all')">전체</button>
          
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Todo from './components/todo';

export default {
  name: 'app',
  data(){
    return{
      userInput:'',
      todoList: [],
      currentState : false,
    };
  },
  computed:{
    activeTodoList(){
      return this.todoList.filter(todo => this.currentState === 'all' || todo.state === this.currentState);
    }
  },
  methods: {
    changeCurrentState(state){
      this.currentState = state; 
    },
    addNewTodo(){
      this.todoList.push({
        label: this.userInput,
        state: false
      });
      this.userInput='';
    },
    toggleTodoState(todo){
      todo.state = !todo.state;
    }
  },
  components: {
    Todo
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #030405;
  margin-top: 60px;
}
</style>
