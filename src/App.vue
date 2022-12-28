<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <!-- v-on: = "함수명" -->
    <TodoInput v-on:addTodo="addTodo"></TodoInput>
    <TodoList v-bind:propsdata="todoItems" @removeTodo="removeItem"></TodoList>
    <!-- v-bind: 프롭스속성이름 = "상위 컴포넌트의 데이터 이름" 상위에서 하위로 전달 -->
    <TodoFooter v-on:removeAll="clearAll"></TodoFooter>
    <!-- removeAll이 발생했을 때 celaerAll 이 실행 -->
  </div>
</template>

<script>
import TodoHeader from "./components/TodoHeader.vue";
import TodoInput from "./components/TodoInput.vue";
import TodoList from "./components/TodoList.vue";
import TodoFooter from "./components/TodoFooter.vue";

export default {
  //name: "App",
  data() {
    return { todoItems: [] }; //스토리지 내용을 집어넣을 빈배열
  },

  components: {
    TodoHeader: TodoHeader,
    TodoInput: TodoInput,
    TodoList: TodoList,
    TodoFooter: TodoFooter,
  },
  // 새로 인식할때 (새로고침) 로컬 스토리지에 남아 있는 내용으로 배열을 만들어 준다
  created: function () {
    if (localStorage.length > 0) {
      for (let i = 0; i < localStorage.length; i++) {
        this.todoItems.push(localStorage.key(i));
      }
    }
  },
  methods:{
    addTodo(todoItem) {
      localStorage.setItem(todoItem, todoItem); 
      this.todoItems.push(todoItem);
    },
    clearAll() {
      localStorage.clear(); // localstorage 에서만 삭제
      this.todoItems= []; // 배열 초기화
    },
    removeItem(todoItem, index) {
      localStorage.removeItem(todoItem)
      this.todoItems.splice(index,1); 
    }
  },
};
</script>

<style>
@font-face {
  font-family: "GmarketSansBold";
  src: url("https://cdn.jsdelivr.net/gh/projectnoonnu/noonfonts_2001@1.1/GmarketSansBold.woff")
    format("woff");
  font-weight: normal;
  font-style: normal;
}

@font-face {
    font-family: 'NanumSquareNeo-Variable';
    src: url('https://cdn.jsdelivr.net/gh/projectnoonnu/noonfonts_11-01@1.0/NanumSquareNeo-Variable.woff2') format('woff2');
    font-weight: normal;
    font-style: normal;
}

.shadow {
  box-shadow: 0 8px 10px rgba(0,0,0,0.08);
}

body {
  background-color: #EEE3CB;
}
#app {
  font-family: 'NanumSquareNeo-Variable', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #967E76;
  max-width: 600px;
  margin: auto;
  padding: 30px 3vw;
}
</style>
