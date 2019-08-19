<template>
  <div id="app">
    <TodoForm v-on:add-todo="addTodo" />
    <TodoList
      v-bind:todos="todos"
      v-on:check="checkTodo"
      v-on:remove="removeTodo"
      v-on:swap="swap"
    />
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import TodoList from './components/TodoList.vue';
import TodoForm from './components/TodoForm.vue';

export default {
  name: 'app',
  components: {
    TodoList,
    TodoForm,
  },
  data() {
    return {
      todos:
      [
        {
          title: 'todo a',
          description: 'content a',
          done: false,
        },
        {
          title: 'todo b',
          description: 'content b',
          done: true,
        },
        {
          title: 'todo c',
          description: 'content c',
          done: false,
        },
      ],
    };
  },
  methods: {
    addTodo(item) {
      this.todos.push(item);
    },
    removeTodo(index) {
      this.todos.splice(index, 1);
    },
    checkTodo({ index, value }) {
      this.todos[index].done = value;
    },
    swap({ a, b }) {
      [this.todos[a], this.todos[b]] = [this.todos[b], this.todos[a]];
    },
  },
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

*, *::before, *::after {
  box-sizing: border-box;
}

.inner {
  width: 600px;
  margin: auto;
}

@media (max-width: 600px) {
  .inner {
    width: 100%;
  }
}

.flex {
  display: flex;
}
.flex.row {
  flex-direction: row;
}
.flex.col {
  flex-direction: column;
}
.grow-1 {
  flex-grow: 1;
}
.flex.just-center {
  justify-content: center;
}
.flex.align-center {
  align-items: center;
}
.flex.align-start {
  align-items: flex-start;
}

.card {
  box-shadow: 1px 1px 0px 0px rgba(0, 0, 0, .2);
  border-radius: 5px;
  border: 1px solid #424242;
  padding: 12px;
}

.item {
  margin-top: 8px;
}

.btn {
  background: inherit;
  padding: 8px 10px;
  border-radius: 5px;
  cursor: pointer;
}
.btn.outlined {
  border: 1px solid #424242;
}
.btn.filled {
  border: none;
  background-color: #424242;
  color: #ffffff;
}
.btn.fullsize {
  width: 100%;
}
.btn:hover {
  box-shadow: 0px 0px 1px 1px rgba(0, 0, 0, .2);
}

input[type="checkbox"] {
  display: none;
}
.checkbox {
  display:inline-block;
  border-radius: 3px;
  margin-right: 12px;
}
.checkbox.unchecked {
  background-color: inherit;
  border: 1px solid #424242;
}
.checkbox.checked {
  background-color: #424242;
  border: none;
}
</style>
