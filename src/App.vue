<template>
  <div id="app">
    <div class="row">
      <div class="wrapper col s12 l10 offset-l1">
        <div class="row">
          <div class="col s12 m6 offset-m3">
            <div class="card">
              <span class="card-title">{{ title }}</span>
              </div>
              <div class="card-content">
                <Todos :todos="todos" @del-todo="deleteTodo"/>
              </div>
              <div class="card-action">
                <AddTodo @add-todo="addTodo" />
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Todos from './components/Todos'
import AddTodo from './components/AddTodo'
import axios from 'axios'

export default {
  name: 'app',
  components: {
    Todos,
    AddTodo
  },
  data() {
    return {
      title: "Todo App",
      todos: []
    }
  },
  methods: {
    deleteTodo(id) {
      axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`)
        .then(res => this.todos = this.todos.filter(todo => todo.id !== id))
        .catch(err => console.log(err));
    },
    addTodo(newTodo) {
      const { title, completed } = newTodo;

      axios.post('https://jsonplaceholder.typicode.com/todos', {
        title,
        completed
      })
        .then(res => this.todos = [...this.todos, res.data])
        .catch(err => console.log(err));
    }
  },
}
</script>

<style lang="scss">


.card {
  margin-top: 35px;
}


</style>
