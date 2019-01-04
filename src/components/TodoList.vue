<template>
    <section>
        <transition-group name="list" tag="ul">
            <!--(todoItem, index) 텍스트 값(key)과 인덱스를 반환하기 위하여 v-for에서 설정해줌-->
            <!--index는 v-for에서 제공해주는 변수-->
            <li v-for="(todoItem, index) in propsdata" :key="todoItem" class="shadow">
                <i class="checkBtn fa fa-check" aria-hidden="true"></i>
                {{ todoItem }}
                <!--@click은 v-on:click과 동일함-->
                <span class="removeBtn" type="button" @click="removeTodo(todoItem,index)">
                    <i class="fa fa-trash-o" aria-hidden="true"></i>
                </span>
            </li>
        </transition-group>
    </section>
</template>
<script>
export default {
    // App.vue에서 받은 todoItems
    props: ['propsdata'],
    // created() App.vue로 이동, todoItems관련은 모두 App.vue에서 처리한다
    // reated(){
    //     if(localStorage.length>0){
    //         for(var i=0; i<localStorage.length; i++){
    //            // localStroage.key() : Passed a number to retrieve nth key of a LocalStorage
    //             this.todoItems.push(localStorage.key(i));
    //         }
    //     }
    // },
    methods: {
        removeTodo(todoItem, index){
            // console.log(todoItem, index);
            // localStorage.removeItem(todoItem);
            // // splice() : 자바스크립트 내장 API
            // // 배열의 특정 인덱스에서 부여한 숫자만큼의 인덱스를 삭제한다
            // // index에 해당되는 원소를 1개 삭제해라
            // this.todoItems.splice(index,1);
            // $emit('이벤트이름')
            // $emit('이벤트이름', 인자1, 인자2 ... ) 이런식으로 인자를 전달할 수 있음
            this.$emit('removeTodo', todoItem, index);
        }
    }
}
</script>
<style>
ul{
    list-style-type: none;
    padding-left: 0px;
    margin-top: 0;
    text-align: left;
}
li{
    display: flex;
    min-height: 50px;
    height: 50px;
    line-height: 50px;
    margin: 0.5rem 0;
    padding: 0 0.9rem;
    background: white;
    border-radius: 5px;
}
.checkBtn{
    line-height: 45px;
    color: #62acde;
    margin-right: 5px;
}
.removeBtn{
    margin-left: auto;
    color: #de4343;
}
.list-enter-active, .list-leave-active{
    transition: all 1s;
}
.list-enter, .list-leave-to{
    opacity: 0;
    transform: translateY(30px);
}
</style>

