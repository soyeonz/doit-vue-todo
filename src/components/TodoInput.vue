<template>
    <div class="inputBox shadow">
        <!--v-model : 폼에 입력한 값을 뷰 인스턴스의 데이터와 즉시 동기화함-->
        <!--v-on : 화면 요소의 이벤트를 감지하여 처리함 -->
        <input type="text" v-model="newTodoItem" placeholder="Type what you have to do"
        v-on:keyup.enter="addTodo"> 
        <span class="addContainer" v-on:click="addTodo">
            <i class="addBtn fa fa-plus" aria-hidden="true"></i>
        </span>
    </div>
</template>
<script>
export default {
    data(){
        return{
            newTodoItem: ''
        }
    },
    methods:{
        addTodo(){
            console.log("start addTodo");
            if(this.newTodoItem !== ""){
                var value = this.newTodoItem && this.newTodoItem.trim();
                //localStorage.setItem(value, value);// key-value로 로컬스토리지에 저장
                // 로컬스토리지에 저장하는 코드를 App.vue로 옮김 
                // $emit으로 할일 텍스트값인 value를 인자로 전달함. -> App.vue의 todoItem
                console.log(value);
                this.$emit('addTodo', value);
                this.clearInput();
            }
        },
        clearInput(){ // 단일 책임 원칙(Single Responsibility Principle) : 함수 하나가 하나의 기능만 담당하도록 설계하는 디자인패턴
            this.newTodoItem = '';
        }
    }
}
</script>
<style scoped>
input:focus {
    outline: none;
}
.inputBox {
    background: white;
    height: 50px;
    line-height: 50px;
    border-radius: 5px;
}
.inputBox input{
    border-style:none;
    font-size: 0.9rem;
}
.addContainer{
    float: right;
    background: linear-gradient(to right, #6478Fb, #8763FB);
    display: block;
    width: 3rem;
    border-radius: 0 5px 5px 0;
}
.addBtn{
    color: white;
    vertical-align: middle;
}
</style>


