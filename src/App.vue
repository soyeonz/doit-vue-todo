<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <!--할일 추가 버튼 클릭시 App컴포넌트로 이벤트 전달-->
    <TodoInput v-on:addTodo="addTodo"></TodoInput>
    <!--todoItems속성을 TodoList컴포넌트에 props로 전달-->
    <!--v-bind: html 기본속성과 뷰 데이터 속성을 연결함-->
    <!--v-on: 이벤트감지-->
    <!--@removeTodo: 삭제 버튼 클릭시 이벤트를 App 컴포넌트에 전달-->
    <TodoList v-bind:propsdata="todoItems" @removeTodo="removeTodo"></TodoList>
    <TodoFooter v-on:removeAll="clearAll"></TodoFooter>
  </div>  
</template>
<script>
// 1. App.vue에 컴포넌트 import
// import로 vue 파일을 가져오는 것은 ES6 방식이다클릭만으로클릭만으로
import TodoHeader from './components/TodoHeader.vue'
import TodoInput from './components/TodoInput.vue'
import TodoList from './components/TodoList.vue'
import TodoFooter from './components/TodoFooter.vue'
// export default : single file components 체계에서 사용하는 ES6 자바스크립트 모듈화 문법, 전역 컴포넌트의 문제점을 해결해준다 (에버노트_Axios 참고)
export default {
  // 하위 컴포넌트에서 공통으로 사용할 todoItems 선언
  // TodoList 컴포넌트에 전달함 (props)
  data(){
    return {
      todoItems: []
    }
  },
  created() {
    if(localStorage.length>0){
      for(var i=0; i<localStorage.length;i++){
        console.log(localStorage.key(i));
        this.todoItems.push(localStorage.key(i));
      }
    }
  },
  methods: {
    addTodo(todoItem){ // addTodo를 emit으로 받아오면서 인자를 받아옴!
      // 로컬 스토리지에 데이터를 추가하는 로직
      localStorage.setItem(todoItem, todoItem);
      this.todoItems.push(todoItem);
    },
    clearAll(){
      localStorage.clear();
      this.todoItems = []; // todoItems 초기화
    },
    removeTodo(todoItem, index){ // 상위컴포넌트에서 인자를 받으면 참고용으로만 활용하고 값을 변경하면 안됨
      localStorage.removeItem(todoItem);
      this.todoItems.splice(index,1);
    }
  },
  // 2. App.vue에 컴포넌트 등록
  components: { // 리터럴 객체? 
    'TodoHeader' : TodoHeader,
    'TodoInput' : TodoInput,
    'TodoList' : TodoList,
    'TodoFooter' : TodoFooter
  }
}
</script>
<style>
body{
    text-align: center; 
    background-color: #F6F6F8;
}
input{
  border-style: groove;
  width: 200px;
}
button{
  border-style: groove;
}
.shadow{
  box-shadow: 5px 10px 10px rgba(0,0,0,0.03);
}
</style>

