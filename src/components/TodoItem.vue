<template>
  <p
    :class="['todo-item', todoProps.completed ? 'is-completed' : '']"
    :id="todoProps.id"
  >
    <input
      type="checkbox"
      :checked="todoProps.completed"
      v-on:change="martItemCompleted"
    />
    {{ todoProps.title }}
    <button class="del-btn" @click="deleteItem">Delete</button>
  </p>
</template>

<script>
// import { ref } from "vue";
export default {
  name: "TodoItem",
  props: ["todoProps"],
  setup(props, context) {
    const martItemCompleted = () => {
      context.emit("item-completed", props.todoProps.id);
    };

    const deleteItem = () => {
      context.emit("delete-item", props.todoProps.id);
    };
    return {
      martItemCompleted,
      deleteItem,
    };
  },
};
</script>

<style scoped>
.todo-item {
  background: #f4f4f4;
  padding: 10px;
  margin: 0;
  border-bottom: 1px #ccc dotted;
}

.is-completed {
  text-decoration: line-through;
}

.del-btn {
  background: #ff0000;
  color: #fff;
  border: none;
  cursor: pointer;
  float: right;
}
</style>
