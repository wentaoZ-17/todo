<template>
  <div id="app">
    <div class="todo-container">
      <div class="todo-wrap">
          <MyHeader @addTodo="addTodo"/>
          <MyList :todos="todos" :checkTodo="checkTodo" :deleteTodo="deleteTodo" />
          <MyFooter :todos="todos" @checkAllTodo="checkAllTodo" @chearAllTodo="chearAllTodo"></MyFooter>
      </div>
    </div>  
  </div>
</template>

<script>
import MyHeader from './components/MyHeader.vue'
import MyFooter from './components/MyFooter.vue'
import MyList from './components/MyList.vue'



export default {
  name: 'App',
  components: {
    MyHeader,
    MyFooter,
    MyList,
  },
  data() {
    return {
      todos: JSON.parse(localStorage.getItem('todos')) || []
    }
  },
  methods: {
    addTodo(todoObj) {
      this.todos.unshift(todoObj)
    },
    //勾选or取消勾选
    checkTodo(id) {
      this.todos.forEach((todo) => {
        if(todo.id === id) todo.done = !todo.done
      })
    },
   //删除一个TODO
    deleteTodo(id) {
      this.todos = this.todos.filter((todo) => {
        return todo.id != id
      })
    },
    // 全选or取消全选
    checkAllTodo(d)
    {
      console.log(d);
      this.todos.forEach(element => {
        element.done = d
      });
    },
    chearAllTodo() {
      this.todos = this.todos.filter((todo)=>!todo.done)
    }
  },
  watch: {
    todos: {
      deep:true,
      handler(value) {
        localStorage.setItem('todos', JSON.stringify(value))
      }
    }
  }
}
</script>

<style>
/* base */
body {
    background-color: #fff;
}
.btn {
    display: inline-block;
    padding: 4px 12px;
    margin-bottom: 0;
    font-size: 14px;
    line-height: 20px;
    text-align: center;
    vertical-align: middle;
    cursor: pointer;
    box-shadow: inset 0 1px 0 rgba(255,255,255,0.2), 0 1px 2px rgba(0, 0,0,0.05);
    border-radius: 4px;
}
.btn-danger{
    color: #fff;
    background-color: #da4f49;
    border: 1px solid #bd362f;
}
.btn-edit{
    color: #fff;
    background-color: skyblue;
    border: 1px solid rgb(77, 203, 253);
    margin-right: 5px;
}
.btn-danger:hover{
    color: #fff;
    background-color: #bd362f;
}
.btn:focus{
    outline: none;
}
.todo-container{
    width: 600px;
    margin: 0 auto;
}
.todo-container .todo-wrap{
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 5px;
}
</style>
