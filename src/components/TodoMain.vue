<script lang="ts">
import TodoAdd from './TodoAdd.vue'
import TodoList from './TodoList.vue'
let No = 1

export default{
  data(){
    return{
      todos: []
    }
  },
  components: {
    TodoAdd,
    TodoList
  },
  props: {
    todo: {}
  },
  methods: {
    addTodo(newTodo){
      const todo = {No: No++, Todo: newTodo, StatusId: 0}
      if(newTodo === '') {
          alert('Todoを入力してください')
          return 
      }
      this.todos.push(todo)
    },
    deleteTodo(no){
      this.todos.splice(no,1)
      console.log(this.todos)
    }
  }
}
</script>

<template>
  <TodoAdd @addTodo="(newTodo) => addTodo(newTodo)"/>
  <TodoList :todos="todos" @deleteTodo="(no) => deleteTodo(no)"/>
</template>

<style scoped>
</style>