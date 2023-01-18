<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" v-on:keyup.enter="addTodo">
    <span class="addContainer" v-on:click="addTodo">
      <i class="fas fa-plus addBtn"></i>
    </span>
  
  <ModalExam v-if="showModal" @close="showModal = false">
    <h3 slot="header">경고!
      <i class="fas fa-times" @click="showModal=false"></i>
    </h3>
    <div slot="body">내용을 입력하세요</div>
    <div slot="footer"></div>
  </ModalExam>
  </div>
</template>

<script>
import ModalExam from "./common/ModalExam.vue";
import {mapMutations} from "vuex";

export default{
  data(){
    return{
      newTodoItem: "",
      showModal:false
    }
  },
  methods: {
    ...mapMutations([
      'addOneItem'
    ]),

    addTodo(){
      if(this.newTodoItem!==''){
        this.addOneItem(this.newTodoItem)
        this.clearInput();
      } else{
        this.showModal=!this.showModal;
      }
    },
    clearInput(){
      this.newTodoItem = "";
    }
  },
  components:{
    ModalExam
  }
}
</script>

<style scoped>
input:focus{
  outline: none;
}

.inputBox{
  background: white;
  height: 50px;
  line-height: 50px;
  border-radius: 5px;
}

.inputBox input{
  border-style: none;
  font-size: 0.9rem;
}

.addContainer{
  float: right;
  background: linear-gradient(to right, #6478fb,#8763fb);
  display: block;
  width: 3rem;
  border-radius: 0 5px 5px 0;
}

.addBtn{
  color: white;
  vertical-align: middle;
}

</style>