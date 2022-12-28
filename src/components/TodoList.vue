<template>
  <div>
    <TransitionGroup name="list" tag="ul">
      <!-- vue 2.2.0 이상에서는 key값 필수 입력 (책에 있는대로 하면 오류)/ propsdata 로 바꿈-->
      <li class="shadow" v-for="(todoItem, index) in propsdata" :key="index">
        <i class="checkBtn fa-solid fa-check"></i>
        <span class="text">{{ todoItem }}</span>
        <span class="removeBtn" @click="removeTodo(todoItem, index)"><i class="fa-solid fa-trash-can"></i></span>
      </li>
    </TransitionGroup>
  </div>
</template>

<script>
export default {
  props: ["propsdata"],  // p. 163
  // **************** App.vue 로 이동
  // data() {
  //   return { todoItems: [] }; //스토리지 내용을 집어넣을 빈배열
  // },
  // **************** App.vue 로 이동
  // created: function () {
  //   if (localStorage.length > 0) {
  //     for (let i = 0; i < localStorage.length; i++) {
  //       this.todoItems.push(localStorage.key(i));
  //     }
  //   }
  // },
  methods: {
    removeTodo:function(todoItem, index){
      //console.log("키: " + index + ", 밸류:" + todoItem);
    this.$emit('removeTodo',todoItem, index);

      /* ******* App.vue 로 이동
      localStorage.removeItem(todoItem)
      this.todoItems.splice(index,1); 
      */
      // 배열에서 삭제
      // .splice() : 배열 특정 항목을 제거
    },
  },
};
</script>

<style scoped>
ul {
  list-style: none;
  padding-left: 0;
  margin-top: 0;
}
li {
  display: flex; 
  justify-content: space-between;
  background: #fff;
  height: 50px;
  line-height: 50px;
  margin: 10px 0;
  border-radius: 5px;
  text-align: left;
  padding-left: 10px;
}
.checkBtn {
  line-height: 50px;
  margin-right: 10px;
  color: #B7C4CF;
}
.removeBtn {
  color: #D7C0AE;
  width: 50px; /* 마우스 반응 영역 정해 주기 */
  text-align:center;
  cursor: pointer;
}
.text {
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  width: 90%;
}

.list-enter-active,
.list-leave-active {
  transition: all 1s ease;
}
.list-enter,
.list-leave-to {
  opacity: 0;
  transform: translateY(30px);
}

</style>