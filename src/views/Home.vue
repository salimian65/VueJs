
<template>
  <div>
    <AddTodo v-on:add-todo="addTodo" />
    <Todos v-bind:todos="todos" v-on:del-todo="deleteTodo" />
    <AutoSize />
    <div>
      <Input1 v-model="num" />
      <button @click="num++">+1</button>
      <p>{{ num }}</p>
    </div>
    <BaseInput @focus="doSomeThing" />
  </div>
</template>
<script>
import Todos from "../components/Todos";
import AddTodo from "../components/AddTodo";
import AutoSize from "../components/AutoSize";
import Input1 from "../components/Input1";
import BaseInput from "../components/BaseInput";

import axios from "axios";
export default {
  name: "Home",
  components: {
    Todos,
    AddTodo,
    AutoSize,
    Input1,
    BaseInput
  },
  data() {
    return {
      todos: [],
      num: 0
    };
  },
  methods: {
    doSomeThing() {
      console.debug("hello");
    },

    deleteTodo(id) {
      axios
        .delete("https://jsonplaceholder.typicode.com/todos/${id}")
        .then((this.todos = this.todos.filter(todo => todo.id !== id)))
        .catch(err => alert(err));
    },

    addTodo(newTodo) {
      const { title, completed } = newTodo;

      axios
        .post("https://jsonplaceholder.typicode.com/todos", {
          title,
          completed
        })
        .then(res => {
          this.todos = [...this.todos, res.data];
          debugger; // eslint-disable-line
          console.debug(this);
        })
        .catch(err => alert(err));
    }
  },
  created() {
    axios
      .get("https://jsonplaceholder.typicode.com/todos?_limit=5")
      .then(res => {
        this.todos = res.data;
        console.log(this);
      })
      .catch(err => alert(err));
  }
};
</script>
<style>
#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
