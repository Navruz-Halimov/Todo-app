<template>
  <div class="todo">
    <div class="todo-inner">
      <form @submit.prevent="addTodo" class="todo-form">
        <div class="todo-form__header">
        <input
          type="text"
          placeholder="Todo Item"
          class="todo-input"
          v-model="newTodo"
        />
        <button
          type="submit"
          name="button"
          class="todo-btn warning"
          :disabled="!newTodo"
          @click="addTodo"
        >
          Add
        </button>
        </div>
        <button name="button" type="button" @click="removeAll()" class="main-btn red">
          Remove All
        </button>
        <button name="button" type="button" @click="allDone()" class="main-btn green">All done</button>
        <button name="button" type="button" @click="allunDone()" class="main-btn warning">All undone</button>
      </form>
      <ul class="todo-list" v-if="todos.length">
        <li v-for="todo in todos" :key="todo.title" class="todo-list__item">
          <div class="todo-list__header">
          <input type="checkbox" v-model="todo.done" :id="todo.title" />
          <label :for="todo.title" :class="{ done: todo.done }" class="todo-title">
            {{todo.title}}
          </label>
          </div>
          <button @click="removeTodo(todo)" name="button" class="remove-btn red">
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
@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;500;700&display=swap');
body{
  font-family: 'Roboto', sans-serif !important;
}
.todo {
  background-image: url("../assets/1.jpg");
  background-size: cover;
  background-repeat: no-repeat;
  height: 100vh;
  &-inner{
    display: flex;
    align-items: flex-start;
    // justify-content: center;
  }
  &-form{
  font-family: 'Roboto', sans-serif !important;
  background-color: #fff;
  padding: 25px;
  min-height: 200px;
  width:300px;
  margin-left: 40px;
  margin-top:16px;
  border-radius: 10px;
  box-shadow: rgba(17, 17, 26, 0.1) 0px 1px 0px,
    rgba(17, 17, 26, 0.1) 0px 8px 24px, rgba(17, 17, 26, 0.1) 0px 16px 48px;
    &__header{
      display: flex;
      width: 100%;
    }
  }
  &-input {
  font-family: 'Roboto', sans-serif !important;
  padding: 10px;
  border: 1px solid #f1b24a;
  border-top-left-radius: 4px;
  border-bottom-left-radius: 4px;
  flex:0 0 75%;
}
&-btn {
    font-family: 'Roboto', sans-serif !important;
  flex:0 0 20%;
  padding: 10px;
  outline: none;
  border: none;
  color:white;
  border-top-right-radius: 4px;
  border-bottom-right-radius: 4px;
  cursor: pointer;
  width: 50px;
  text-align: center;
&:disabled{
  cursor: not-allowed !important;
}
}
&-list {
  list-style-type: none;
  margin-left: 30px;
  background-color: #fff;
  padding: 25px;
  min-height: 200px;
  min-width: 300px;
  border-radius: 10px;
  box-shadow: rgba(17, 17, 26, 0.1) 0px 1px 0px,
    rgba(17, 17, 26, 0.1) 0px 8px 24px, rgba(17, 17, 26, 0.1) 0px 16px 48px;
    &__item{
      display: flex;
      justify-content: space-between;
      margin: 10px 0;
    }
    &__header{
      display: flex;
      align-items: center;
    }
}
&-title {
  margin-left: 5px;
  margin-right: 5px;
}
&-input:focus {
  outline: none;
  border: 1px solid rgb(117, 235, 20);
  box-shadow: rgba(17, 17, 26, 0.1) 0px 4px 16px,
    rgba(17, 17, 26, 0.05) 0px 8px 32px;
}

.done {
  text-decoration: line-through;
}
.remove-btn {
  font-family: 'Roboto', sans-serif !important;
  border: none;
  padding: 5px;
  border-radius: 4px;
  cursor: pointer;
  color:white;
  &:focus {
    outline: none;
  }
}
.main-btn{
  font-family: 'Roboto', sans-serif !important;
  border: none;
  padding: 6px;
  color:white;
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
.red{
  background-color: #f44336;
}
.green{
  background-color: #4CAF50;
}
.warning{
  background-color: #ff9800;;
}
}
</style>
