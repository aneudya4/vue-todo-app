<template>
  <header class="header">
    <div class="forms">
      <p>TODO</p>

      <form @submit.prevent="onSubmit">
        <input type="text" placeholder="Go to the gym" v-model="todoTitle" />
      </form>
    </div>
  </header>
</template>

<script>
export default {
  name: "Header",

  data() {
    return {
      todoTitle: "",
      inputError: false,
    };
  },

  methods: {
    onSubmit() {
      if (this.todoTitle.trim() !== "") {
        const newTodo = {
          id: new Date().getUTCMilliseconds(),
          todoTitle:
            this.todoTitle.charAt(0).toUpperCase() +
            this.todoTitle.toLowerCase().slice(1),
          isCompleted: false,
        };
        this.$emit("add-todo", newTodo);

        this.todoTitle = "";
        this.inputError = false;
      } else {
        this.inputError = true;
      }
    },
  },
};
</script>

<style scoped lang="scss">
.header {
  position: relative;
  font-family: sans-serif;
  width: 100%;
  height: 35vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background-image: url("../assets/background.jpeg");
  background-size: cover;
  background-position: 25% 47%;

  &::before {
    position: absolute;
    display: block;
    content: "";
    width: 102%;
    height: 100%;
    background: rgb(129, 18, 131);
    background: linear-gradient(
      90deg,
      rgba(129, 18, 131, 0.8645833333333334) 0%,
      rgba(147, 16, 177, 1) 0%,
      rgba(147, 16, 177, 1) 17%,
      rgba(11, 194, 243, 1) 99%,
      rgba(79, 82, 172, 0.20351890756302526) 100%,
      rgba(2, 0, 36, 1) 100%
    );
    opacity: 0.7;
  }

  .forms {
    z-index: 1;

    p {
      color: white;
      letter-spacing: 15px;
      margin-bottom: 20px;
      font-size: 30px;
      font-weight: bold;
    }
    input {
      width: 600px;
      padding: 15px 20px;
      border-radius: 5px;
      border: none;
      font-size: 20px;
      outline: none;

      &::placeholder {
        color: #cbcbca;
      }
    }
  }
}
</style>
