<template>
  <div id="app" class="container">
    <div class="card card-body bg-light">
      <div class="title">mangojeoong's 투두두두두</div>
    </div>

    <div class="card card-default card-borderless">
      <div class="card-body">
        <!-- !!! 문제 전제조건!!!
              모든 이벤트 처리 App.vue에서 실행!!
              -->
        <!-- 
        -케밥st-로 적는거 불편;
        자식 add-todo 이벤트 올라오면 -> 보모는 addTodo function 실행
        -->
        <InputTodo @add-todo="addTodo" />
        <!-- 
        1. inputTodo.vue에서 emit으로 받은 배열을 다시 TodoList.vue로 전달해야함
        2. TodoList.vue에서 다시 emit으로 삭제, 토글 이벤트 올리면 핸들링 함수 실행
        -->
        <TodoList
          :todoList="todoList"
          @delete-todo="deleteTodo"
          @toggle-completed="toggleCompleted"
        />
      </div>
    </div>
  </div>
</template>

<script>
import TodoList from "./components/TodoList.vue";
import InputTodo from "./components/InputTodo.vue";

let ts = new Date().getTime(); //todolist 배열 객체 속성 id로 쓰임

export default {
  name: "App",
  components: { InputTodo, TodoList }, //쓸 component 불러오기

  data() {
    return {
      todoList: [
        { id: ts, todo: "자전거 타기", completed: false },
        { id: ts + 1, todo: "공원 산책", completed: true },
        { id: ts + 2, todo: "카페 가기", completed: false },
        { id: ts + 3, todo: "Vue 원고 집필", completed: false },
      ],
    };
  },

  methods: {
    /* 
    적용점
    - 뭐라도 입력해야 올라가도록 todo.length에 따른 조건문 설정 
    -Reference) SFC assignment basic lv. Input 과제  
*주의: InputTodo.vue에서 문자열 todo 그대로 전달받았음
    */
    addTodo(todo) {
      if (todo.length >= 1) {
        this.todoList.push({
          // list 맨 뒤에 넣어주기
          // 문제상황: id: ts 라고 작성했더니 처음 투두 불러올때 넘버에서 변하질 않음
          // -> delete하고 다시 todolist push하다보면 넘버링 꼬여서 이상해짐
          // -> findIndex할때도 문제 생김
          // -> conclusion: id에는 할때마다 새로운 값 생성하도록 해야된다
          id: new Date().getTime(),
          todo,
          completed: false,
        });
      }
    },

    //자식에서 id값(int형) 그대로 받음
    deleteTodo(id) {
      const i = this.todoList.findIndex((t) => t.id === id);
      this.todoList.splice(i, 1); // 1개 삭제 안 하고 그냥 splice(i)했더니 i부터 다 사라짐
      console.log("deleteTodo() 함수 실행");
    },
    //자식에서 id값(int형) 그대로 받음
    toggleCompleted(id) {
      console.log("toggleCompleted() 함수 실행");
      const i = this.todoList.findIndex((t) => t.id === id);
      this.todoList[i].completed = !this.todoList[i].completed;
    },
  },
};
</script>
