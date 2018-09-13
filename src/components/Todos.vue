<template>
  <div class="todos">
    <h2>{{title}}</h2>
    <div>
      <input type="text" v-model="newTodo" @keyup.enter="addTodo">
    </div>
    <todo todoList="todosList"/>
    <div class="todoItem">
        <div v-for="item in todosList" :key="item.id">
            <input type="checkbox" v-model="item.isCompleted">
            <input type="text" 
              v-bind:readonly="item.isCompleted" 
              v-bind:class="{completedTodo: item.isCompleted}" 
              v-model="item.title" 
              >
            <button @click="removeTodo(item.id)">&times;</button>
        </div>
    </div>
  </div>
</template>

<script>
import Todo from './Todo'
import TodoModel from '../models/todo.model'
import func from './vue-temp/vue-editor-bridge';

export default {
  name: 'Todos',
  props: {
    title: String,
  },
  components: {
    Todo
  },
  data() {
    return {
      newTodo: '',
      todosList: todoStorage.fetch()
    }
  },
  methods: {
    addTodo: function() {
      let a = this.newTodo;
      if (!a) return;
      let b = new TodoModel({
        id: 1,
        title: this.newTodo
      });
      this.todosList.push(b);
      todoStorage.save(this.todosList);
      this.newTodo = '';
    },
    removeTodo: function(index) {
      this.todosList.splice(index, 1);
      todoStorage.save(this.todosList);
    },
    editTodo: function(index, title) {
      
    }
  }
}

var todoStorage = {
  fetch: function () {
    var todos = JSON.parse(localStorage.getItem('vuejsTodo') || '[]')
    todos.forEach(function (todo, index) {
      todo.id = index
    })
    todoStorage.uid = todos.length
    return todos
  },
  save: function (todos) {
    localStorage.setItem('vuejsTodo', JSON.stringify(todos))
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
.completedTodo {
  text-decoration: line-through;
  border: none;
}
</style>
