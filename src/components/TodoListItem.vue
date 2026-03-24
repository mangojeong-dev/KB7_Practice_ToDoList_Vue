<template>
  <li
    class="list-group-item"
    :class="{ 'list-group-item-success': todoItem.completed }"
    @click="$emit('toggle-completed', todoItem.id)"
  >
    <!-- todo-done 클래스 background-color 변경 - main.css 정의 -->
    <span class="pointer" :class="{ 'todo-done': todoItem.completed }">
      {{ todoItem.todo }}
    </span>

    <!-- botstpap 버튼 사용
    li 전체 클릭 시 -> 완료토글
    내부의 삭제 버튼 클릭 시 -> 삭제
    @click.stop으로 버블링 안 막으면 삭제,완룥토글 같이 실행됨 -->
    <span
      class="float-end badge bg-danger pointer"
      @click.stop="$emit('delete-todo', todoItem.id)"
    >
      삭제
    </span>
  </li>
</template>

<script>
export default {
  name: "TodoListItem",
  // 객체(obj로 전달
  props: {
    todoItem: { Object },
  },

  emits: ["delete-todo", "toggle-completed"],
};
</script>
