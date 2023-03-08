<template>
  <div id="container">
    <TodoHeader></TodoHeader>
    <TodoInput v-on:addTodo="addTodo"></TodoInput>
    <TodoList v-bind:todos="todos"></TodoList>
    <TodoFooter></TodoFooter>
  </div>
</template>

<script>
import "./assets/reset.css";
import TodoList from "./components/TodoList.vue";

import TodoHeader from "./components/TodoHeader.vue";

import TodoInput from "./components/TodoInput.vue";

import TodoFooter from "./components/TodoFooter.vue";
export default {
  name: "App",
  data() {
    return {
      todos: [], //{id:0, text:'할일', modify:false}
      id: 0,
    };
  },
  methods: {
    addTodo(text) {
      this.todos.push({ id: this.id, text: text, modify: false });
      this.id++;
    },
  },
  components: {
    TodoHeader: TodoHeader,
    TodoInput: TodoInput,
    TodoList: TodoList,
    TodoFooter: TodoFooter,
  },
};
</script>

<style scoped>
#container {
  max-width: 500px;
  margin: 50px auto;
}
</style>
