<template>
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

export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Todos",
  components: {
    TodoItem,
  },
  setup() {
    const todos = ref([
      {
        id: 1,
        title: "Viec 1",
        completed: false,
      },
      {
        id: 2,
        title: "Viec 2",
        completed: true,
      },
      {
        id: 3,
        title: "Viec 3",
        completed: false,
      },
    ]);

    const markComplete = (id) => {
      todos.value = todos.value.map((todo) => {
        if (todo.id === id) {
          todo.completed = !todo.completed;
        }
        return todo;
      });
    };

    const deleteTodo = (id) => {
      todos.value = todos.value.filter((todo) => {
        return todo.id !== id;
      });
    };
    return {
      todos,
      markComplete,
      deleteTodo,
    };
  },
};
</script>

<style></style>
