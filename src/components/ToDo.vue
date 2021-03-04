<template>
  <div class="wrapper">
    <div class="todo-inner">
      <form @submit.prevent="addTodo">
        <label for="newTodo"></label>
        <input
          type="text"
          placeholder="ToDo item"
          class="todo-input"
          v-model="newTodo"
        />
        <button
          type="submit"
          name="button"
          class="todo-btn"
          :disabled="!newTodo"
          @click="addTodo"
        >
          Add
        </button>
        <button name="button" type="button" @click="removeAll()" class="main-btn">
          Remove All
        </button>
        <button name="button" type="button" @click="allDone()" class="main-btn">All done</button>
        <button name="button" type="button" @click="allunDone()" class="main-btn">All undone</button>
      </form>
      <ul class="todo-list" v-if="todos.length">
        <li v-for="todo in todos" :key="todo.title">
          <input type="checkbox" v-model="todo.done" />
          <span :class="{ done: todo.done }" class="todo-title">{{
            todo.title
          }}</span>
          <button @click="removeTodo(todo)" name="button" class="remove-btn">
            Remove
          </button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos: [],
      newTodo: "",
    };
  },
  methods: {
    addTodo() {
      this.todos.push({
        title: this.newTodo,
        done: false,
      });
      this.newTodo = "";
      console.log(this.todos);
    },
    removeTodo(todo) {
      const todoIndex = this.todos.indexOf(todo);
      this.todos.splice(todoIndex, 1);
    },
    removeAll() {
      this.todos = "";
    },
    allDone(){
      this.todos.forEach(todo => {
        todo.done=true;
      });
    },
    allunDone(){
      this.todos.forEach(todo=>{
        todo.done=false;
      })
    }
  },
};
</script>

<style lang="scss">
.wrapper {
  background-image: url("../assets/1.jpg");
  background-size: cover;
  background-repeat: no-repeat;
  height: 100vh;
}
.done {
  text-decoration: line-through;
}
.todo-inner {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
}
form {
  background-color: #fff;
  padding: 25px;
  height: 200px;
  border-radius: 10px;
  box-shadow: rgba(17, 17, 26, 0.1) 0px 1px 0px,
    rgba(17, 17, 26, 0.1) 0px 8px 24px, rgba(17, 17, 26, 0.1) 0px 16px 48px;
}
.todo-input {
  padding: 5px;
  border: 1px solid #f1b24a;
  border-top-left-radius: 4px;
  border-bottom-left-radius: 4px;
}
.todo-input:focus {
  outline: none;
  border: 1px solid rgb(117, 235, 20);
  box-shadow: rgba(17, 17, 26, 0.1) 0px 4px 16px,
    rgba(17, 17, 26, 0.05) 0px 8px 32px;
}
.todo-btn {
  padding: 6px;
  background-color: #f1b24a;
  outline: none;
  border: none;
  border-top-right-radius: 4px;
  border-bottom-right-radius: 4px;
  cursor: pointer;
  width: 50px;
  text-align: center;
}
.todo-list {
  list-style-type: none;
  margin-left: 30px;
  background-color: #fff;
  padding: 25px;
  height: 200px;
  border-radius: 10px;
  box-shadow: rgba(17, 17, 26, 0.1) 0px 1px 0px,
    rgba(17, 17, 26, 0.1) 0px 8px 24px, rgba(17, 17, 26, 0.1) 0px 16px 48px;
}
.todo-title {
  margin-left: 5px;
  margin-right: 5px;
}
.remove-btn {
  border: none;
  background-color: #f1b24a;
  padding: 5px;
  border-radius: 4px;
  cursor: pointer;
  &:focus {
    outline: none;
  }
}
.main-btn{
  border: none;
  padding: 6px;
  background-color: #f1b24a;
  cursor: pointer;
  display: block;
  margin-top: 10px;
  border-radius: 4px;
  &:hover{
      box-shadow: rgba(17, 17, 26, 0.1) 0px 1px 0px,
    rgba(17, 17, 26, 0.1) 0px 8px 24px, rgba(17, 17, 26, 0.1) 0px 16px 48px;
  }
  &:focus{
    outline: none;
  }
}
</style>
