<template>
  <ul class="list-group">
    <TodoListItem
      v-for="todoItem in todoList"
      :key="todoItem.id"
      :todoItem="todoItem"
      @delete-todo="$emit('delete-todo', $event)"
      @toggle-completed="$emit('toggle-completed', $event)"
    />
  </ul>
</template>

<script>
import TodoListItem from "./TodoListItem.vue";

export default {
  name: "TodoList",
  // TodoListItem  -> TodoList -> App 토스
  components: { TodoListItem },
  // 부모에게서 받는다ㅣ
  props: {
    todoList: {
      type: Array,
      required: true,
    },
  },

  emits: ["delete-todo", "toggle-completed"],
};
</script>
