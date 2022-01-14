<template>
  <div class="todo-container">
    <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
    <div class="todo-wrap">
      <Header :addTodo="addTodo" />
      <List :todos="todos" :deleteTodo="deleteTodo" :updateTodo="updateTodo" />
      <Footer :todos="todos" :selectAll="selectAll" :deleteCompleted="deleteCompleted" />
    </div>
  </div>
  
  
</template>

<script>
import Header from './components/Header.vue'
import List from './components/List.vue'
import Footer from './components/Footer.vue'

export default {
  name: 'App',
  components: {
    Header,
    List,
    Footer,
  },
  data() {
    return {
      todos:JSON.parse(localStorage.getItem('todos_key')|| '[]')
      // todos:[
      //   {id:1,title:'111',complete:false},
      //   {id:2,title:'222',complete:true},
      //   {id:3,title:'333',complete:false}
      // ]
    }
  },
  watch:{
    //一般watch
    // todos:function (value) {
    //   console.log('watch',value)
    //   // localStorage.setItem('todos_key', JSON.stringify(value))
    // }
    //深度watch
    todos: {
      deep: true, // 深度监视: 内部发生任何变化都会回调
      handler: function (value) {  // todos发生了变化
        console.log('deep watch')
        // 保存todos
        localStorage.setItem('todos_key', JSON.stringify(value))
      },
    }
  },
  methods: {
    addTodo(todo) {
      console.log(todo);
      this.todos.unshift(todo);
    },
    deleteTodo(index) {
      this.todos.splice(index,1)
    },
    updateTodo(todo, complete) {
      console.log('updateTodo')
      todo.complete = complete
    },
    //全选/全不选
    selectAll(isChecked) {
      this.todos.forEach(todo=>todo.complete = isChecked)
    },
    /* 删除已完成的（及留下未完成的） */
    deleteCompleted() {
      this.todos = this.todos.filter(todo => !todo.complete)
    }
  },
}
</script>

<style>
/*app*/
  .todo-container {
    width: 600px;
    margin: 0 auto;
  }
  .todo-container .todo-wrap {
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 5px;
  }
</style>
