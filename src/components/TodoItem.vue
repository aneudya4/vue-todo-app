<template>
  <li>
    <div class="todo" ref="todoRef">
      <input
        class="checkbox"
        type="checkbox"
        :checked="todo.isCompleted"
        @change="handleCheck"
      />
      <p :class="{ completed: todo.isCompleted }">{{ todo.todoTitle }}</p>
      <span @click="handleDelete"> &#x2715; </span>
    </div>
  </li>
</template>

<script>
export default {
  name: "TodoItem",

  props: {
    todo: Object,
  },

  data() {
    return {
      completed: false,
    };
  },

  methods: {
    handleDelete(e) {
      this.$refs.todoRef.classList.add("animate");
      setTimeout(() => {
        this.$emit("delete-todo", this.todo.id);
      }, 800);
    },

    handleCheck() {
      this.completed = !this.completed;
      this.$emit("update-completed", this.todo.id);
    },
  },
};
</script>

<style scoped lang="scss">
.todo {
  width: 100%;
  font-size: 20px;
  display: flex;
  align-items: center;

  p {
    margin-left: 20px;
    font-family: arial;
    font-weight: lighter;
    color: #6b6968;
    &.completed {
      text-decoration: line-through;
      color: lightgray;
    }
  }

  span {
    display: none;
    align-self: flex-end;
    margin-left: auto;
    &:hover {
      color: red;
    }
  }
}

li {
  padding: 20px 40px;
  cursor: pointer;

  &:hover {
    div {
      transform: scale(1.1);
      transition: all ease 0.3s;
    }
  }

  &:input {
    cursor: pointer;
  }

  &:not(:last-child) {
    border-bottom: 1px solid lightgray;
  }

  /* animation  for  checkbox*/
  .checkbox {
    -webkit-appearance: none;
    -moz-appearance: none;
    -ms-appearance: none;
    appearance: none;
    height: 25px;
    width: 25px;
    transition: all 0.15s ease-out 0s;
    background: white;
    border: 1px solid #cccbcb;
    color: rgba(9, 119, 192, 0.884);
    outline: none;
    border-radius: 50%;
    border-radius: 50;
    cursor: pointer;
  }
  .checkbox:hover {
    background: #cbcbca;
  }
  .checkbox:checked {
    background: white;
    border-radius: 0;
    border: none;
  }
  .checkbox:checked::before {
    height: 20px;
    width: 20px;
    position: absolute;
    content: "✔";
    display: inline-block;
    font-size: 26.66667px;
    text-align: center;
  }
  .checkbox:checked::after {
    border-radius: 50%;
    animation: click-wave 0.65s;
    background: rgba(9, 119, 192, 0.884);
    content: "";
    display: block;
    z-index: 2;
  }

  div.animate {
    position: relative !important;
    animation-name: slide;
    animation-duration: 1.2s;
  }

  @keyframes slide {
    0% {
      left: 0px;
    }

    35% {
      opacity: 0.3;
    }
    45% {
      opacity: 0.2;
    }

    75% {
      opacity: 0;
    }

    100% {
      left: 1000px;
      opacity: 0;
    }
  }

  /* animate checkbox when clicked */
  @keyframes click-wave {
    0% {
      height: 40px;
      width: 40px;
      opacity: 0.35;
      position: relative;
    }
    100% {
      height: 200px;
      width: 200px;
      margin-left: -80px;
      margin-top: -80px;
      opacity: 0;
    }
  }
}
</style>
