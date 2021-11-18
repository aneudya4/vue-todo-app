<template>
  <section class="container">
    <div class="todos">
      <ul>
        <TodoItem
          v-if="showAll"
          v-for="todo in todos"
          :key="todo.id"
          :todo="todo"
          @delete-todo="deleteTodo"
          @update-completed="updateTodo"
        />
        <TodoItem
          v-if="isShowingActive"
          v-for="todo in activeTodos"
          :key="todo.id"
          :todo="todo"
          @delete-todo="deleteTodo"
          @update-completed="updateTodo"
        />

        <TodoItem
          v-if="isShowingCompleted"
          v-for="todo in completedTodos"
          :key="todo.id"
          :todo="todo"
          @delete-todo="deleteTodo"
          @update-completed="updateTodo"
        />
      </ul>
    </div>
    <div class="menu">
      <div class="todos__left">
        {{ filterCompletedTodos.length }} items left
      </div>
      <div class="menu__list">
        <ul class="action">
          <li :class="{ all: showAll }" @click="handleShowAll">All</li>
          <li :class="{ active: isShowingActive }" @click="handleShowActive">
            Active
          </li>
          <li
            :class="{ completed: isShowingCompleted }"
            @click="handleShowCompleted"
          >
            Completed
          </li>
        </ul>
      </div>
      <div class="action">
        <span @click="clearCompleted">Clear Completed</span>
      </div>
    </div>
  </section>
</template>

<script>
import TodoItem from "./TodoItem.vue";
export default {
  name: "Todos",
  components: {
    TodoItem,
  },
  props: {
    todos: Array,
  },

  data() {
    return {
      showAll: true,
      isShowingCompleted: false,
      isShowingActive: false,
    };
  },

  computed: {
    filterCompletedTodos: function () {
      return this.todos.filter((todo) => !todo.isCompleted);
    },

    completedTodos() {
      return this.todos.filter((todo) => todo.isCompleted);
    },

    activeTodos() {
      return this.todos.filter((todo) => !todo.isCompleted);
    },
  },

  methods: {
    updateTodo(todoId) {
      this.$emit("update-todo", todoId);
    },

    deleteTodo(todoId) {
      this.$emit("remove-todo", todoId);
    },

    clearCompleted() {
      this.$emit("clear-completed");
    },

    handleShowAll() {
      this.showAll = true;
      this.isShowingActive = false;
      this.isShowingCompleted = false;
    },

    handleShowCompleted() {
      if (this.completedTodos.length) {
        this.showAll = false;
        this.isShowingActive = false;
        this.isShowingCompleted = true;
      }
    },

    handleShowActive() {
      if (this.activeTodos.length) {
        this.showAll = false;
        this.isShowingCompleted = false;
        this.isShowingActive = true;
      }
    },
  },
};
</script>

<style lang="scss">
.container {
  width: 600px;
  margin: 0 auto;
  height: 400px;
  position: relative;
  top: -100px;
  background-color: #fff;
  border-radius: 10px;
  font-family: arial;
  font-weight: lighter;
  & .todos {
    background-color: white;
    border: 1px solid lightgray;
    // border-radius: 10px;
    border-top-left-radius: 5px;
    border-top-right-radius: 5px;
  }

  & .menu {
    display: flex;
    justify-content: space-between;
    padding: 20px;
    border: 1px solid lightgray;
    border-top: none;
    color: gray;
    border-bottom-left-radius: 5px;
    border-bottom-right-radius: 5px;
    .action > * {
      cursor: pointer;

      &:hover {
        color: #1da1f2;
      }
    }

    ul {
      margin-right: auto;
      display: flex;
      align-self: center;

      li.active,
      li.completed,
      li.all {
        color: #1da1f2;
      }

      li:nth-child(2) {
        margin: 0 20px;
      }
    }
  }

  li:hover {
    span {
      display: block !important;
      cursor: pointer;
    }
  }
}
</style>
