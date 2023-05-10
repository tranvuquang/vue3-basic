<template>
  <AddTodo @add-todo="addTodo" />
  <TodoItem
    v-for="todo in todos"
    v-bind:key="todo.id"
    :todoProps="todo"
    v-on:item-completed="markComplete"
    @delete-item="deleteTodo"
  />
</template>

<script>
import { ref } from "vue";
import TodoItem from "./TodoItem.vue";
import AddTodo from "./AddTodo.vue";
import axios from "axios";

export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Todos",
  components: {
    TodoItem,
    AddTodo,
  },
  setup() {
    const todos = ref([
    ]);

    const getAllTodos = async () => {
      try {
        const res = await axios.get(
          "https://jsonplaceholder.typicode.com/todos?_limit=5"
        );
        todos.value = res.data;
      } catch (error) {
        console.log(error);
      }
    };

    getAllTodos();

    const markComplete = (id) => {
      todos.value = todos.value.map((todo) => {
        if (todo.id === id) {
          todo.completed = !todo.completed;
        }
        return todo;
      });
    };

    const deleteTodo = async (id) => {
      try {
        await axios.delete(`https://jsonplaceholder.typicode.com/todos/${id}`);
        todos.value = todos.value.filter((todo) => todo.id !== id);
      } catch (error) {
        console.log(error);
      }
    };

    const addTodo = async (newTodo) => {
      try {
        const res = await axios.post(
          "https://jsonplaceholder.typicode.com/todos",
          newTodo
        );
        todos.value.push(res.data);
      } catch (error) {
        console.log(error);
      }
    };
    return {
      todos,
      markComplete,
      deleteTodo,
      addTodo,
    };
  },
};
</script>

<style></style>
