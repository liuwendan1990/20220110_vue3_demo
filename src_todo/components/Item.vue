<template>
  <li @mouseenter="handleEnter(true)"
      @mouseleave="handleEnter(false)">
    <label>
      <input type="checkbox" v-model="isChecked"/>
      <span>{{todo.title}}</span>
    </label>
    <button class="btn btn-danger" v-show="isShow" @click="deleteItem">删除</button>
  </li>
</template>

<script>
export default {
  name: 'Item',
  props:{
    todo:Object,
    index:Number,
    deleteTodo:Function,
    updateTodo:Function
  },
  data() {
    return {
      isShow:false,
      // bgColor:''
    }
  },
  computed:{
    isChecked: {
      get () {// checkout是否勾选, 看接收的todo是否已经完成
        return this.todo.complete
      },

      set (value) {// 当用户操作checkbox界面时调用
        this.updateTodo(this.todo, value)
      }
    }
  },
  methods: {
    handleEnter(isEnter) {
      if(isEnter){
        this.isShow = true
      }else{
        this.isShow = false
      }
    },
    deleteItem() {
       if (confirm('确定删除吗?')) {
          this.deleteTodo(this.index)
       }
    }
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
/*item*/
  li {
    list-style: none;
    height: 36px;
    line-height: 36px;
    padding: 0 5px;
    border-bottom: 1px solid #ddd;
  }
  li:hover {
    background-color: #ccc;
  }
  li label {
    float: left;
    cursor: pointer;
  }
  
  li label li input {
    vertical-align: middle;
    margin-right: 6px;
    position: relative;
    top: -1px;
  }
  
  li button {
    float: right;
    margin-top: 3px;
  }
  
  li:before {
    content: initial;
  }
  
  li:last-child {
    border-bottom: none;
  }
</style>
