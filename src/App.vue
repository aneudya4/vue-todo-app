<template>
  <Header @add-todo="addTodo" />
  <Todos
    v-if="todos.length"
    :todos="todos"
    @remove-todo="RemoveTodo"
    @clear-completed="removeCompleted"
    @update-todo="completeTodo"
  />
</template>

<script>
import Header from "./components/Header.vue";
import Todos from "./components/Todos.vue";

import "./assets/global.css";
export default {
  name: "App",
  components: {
    Header,
    Todos,
  },

  data() {
    return {
      todos: [],
    };
  },

  methods: {
    addTodo(newTodo) {
      this.todos = [...this.todos, newTodo];
    },

    RemoveTodo(todoId) {
      this.todos = this.todos.filter((todo) => todo.id !== todoId);
    },

    removeCompleted() {
      this.todos = this.todos.filter((todo) => !todo.isCompleted);
    },

    completeTodo(todoId) {
      console.log(todoId, "mss");
      this.todos = this.todos.map((todo) => {
        if (todo.id === todoId) {
          todo.isCompleted = !todo.isCompleted;
          return todo;
        }
        return todo;
      });
    },
  },
};
</script>

<style lang="scss"></style>
