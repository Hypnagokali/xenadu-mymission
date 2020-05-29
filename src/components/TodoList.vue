<template>
<div>
  <h2 class="header">Meine App: {{ msg }}</h2>
  <div class="todo-container input-controll-container">
    <label for="task-input">Was ist zu tun?</label>

    <input
    v-on:keyup.enter="addItem"
    v-model="newTodo"
    class="task-input"
    placeholder="Staubsaugen ..."
    name="task-input"
    type="text">

  </div>
  <div class="todo-container todo-item-container">
    <TodoItem
      v-for="todo in todos"
      v-bind:key="todo.id"
      v-bind:task="todo.name"
      v-bind:checked.sync="todo.done"
    >
    </TodoItem>
  </div>
</div>
</template>

<script>
import TodoItem from './TodoItem.vue';

export default {
  components: {
    TodoItem,
  },
  name: 'TodoList',
  props: {
    msg: String,
  },
  data() {
    return {
      nextId: 4,
      test: 'ich bin ein test',
      todos: [
        { id: 1, name: 'Kaffee etc...', done: true },
        { id: 2, name: 'Projekt umbenennen', done: false },
        { id: 3, name: 'Staubsaugen', done: false },
      ],
      newTodo: '',
    };
  },
  methods: {
    addItem() {
      console.log(`add item: ${this.newTodo}`);
      // create new todo-object
      const todo = {
        id: this.nextId,
        name: this.newTodo,
        done: false,
      };
      this.todos.push(todo);
      this.nextId += 1;
      localStorage.setItem('todos', JSON.stringify(this.todos));
      localStorage.setItem('nextId', this.nextId);
      this.newTodo = '';
    },
  },
  created() {
    if (localStorage.getItem('todos') === null) return;
    this.todos = JSON.parse(localStorage.getItem('todos'));
    this.nextId = localStorage.getItem('nextId');
    const updatedList = [];
    this.todos.forEach((element, index) => {
      console.log('nächstes Element löschen?');
      console.log(`Element: ${element.name} mit Index: ${index}`);
      if (!element.done) {
        console.log(`lösche ${element.name} mit Index: ${index}`);
        updatedList.push(element);
      }
    });
    this.todos = updatedList;
  },
  updated() {
    console.log('Update Hook triggered!');
    localStorage.setItem('todos', JSON.stringify(this.todos));
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
* {
  box-sizing: border-box;
}
h3 {

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

.task-input {
  width: 100%;
  font-size: 20px;
}

.todo-container {
  margin: 20px;
}

input[type=text], textarea {
  -webkit-transition: all 0.30s ease-in-out;
  -moz-transition: all 0.30s ease-in-out;
  -ms-transition: all 0.30s ease-in-out;
  -o-transition: all 0.30s ease-in-out;
  outline: none;
  padding: 3px 0px 3px 3px;
  margin: 5px 1px 3px 0px;
  border: 1px solid #DDDDDD;
}
input[type=text]:focus, textarea:focus {
  box-shadow: 0 0 5px #42ff04;
  padding: 3px 0px 3px 3px;
  margin: 5px 1px 3px 0px;
  border: 1px solid #00ad0d;
}
</style>
