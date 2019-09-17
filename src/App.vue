<template>
  <div id="app">
    <Header />
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
  </div>
</template>

<script>
import Todos from './components/Todos';
import Header from './components/Header';
import AddTodo from './components/AddTodo';
import axios from 'axios';

export default {
  name: 'app',
  components: {
    Todos,
    Header,
    AddTodo
  },
  data() {
    return({
      todos: []
    })
  },
  methods:{
    deleteTodo(id) {
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
      .then(
      // eslint-disable-next-line  
      res => this.todos = this.todos.filter(todo => todo.id !== id))
      .catch(err => 
      // eslint-disable-next-line
      console.log(err))
    },
    addTodo(newTodo) {
      const { title, completed } = newTodo

      axios.post('https://jsonplaceholder.typicode.com/todos', {
        title,
        completed
      })
      .then( res => this.todos = [...this.todos, res.data] )
      .catch( err => 
      // eslint-disable-next-line
      console.log(err))

      
    }
  },
  created() {
    axios.get('https://jsonplaceholder.typicode.com/todos?_limit=3')
      .then(res => this.todos = res.data)
      .catch(err => 
      // eslint-disable-next-line
      console.log(err))
  }
}
</script>

<style>
  *{
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  body{
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.4;
  }
</style>
