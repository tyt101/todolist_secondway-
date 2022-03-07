<template>
<div id="app">
  <TodoHeader ></TodoHeader>
  <TodoMain :list="list" ></TodoMain>
  <TodoFooter :list="list" ></TodoFooter>
</div>
</template>

<script>
import TodoHeader from './components/TodoHeader'
import TodoMain from './components/TodoMain'
import TodoFooter from './components/TodoFooter'
export default {
  name: 'App',
  components: {
    TodoHeader,
    TodoMain,
    TodoFooter
  },
  data() {
    return {
      list:[]
    }
  },
  
  methods: {
    getTask(task){
      this.list.push(task)
    },
    deleteTaskF(taskId){
      this.list = this.list.filter(task=>{
          return task.id!=taskId
      })
    },
    changeTasks(ischeck){
      this.list.forEach(li=>{
        li.isDone=ischeck
      })
    },
    clearAll(){
      this.list=this.list.filter(li=>{
        return !li.isDone
      })
    }
  },
  mounted() {
    this.$bus.$on('deleteList',this.deleteTaskF)
    this.$bus.$on('addTask',this.getTask)
    this.$bus.$on('change',this.changeTasks)
    this.$bus.$on('clearAll',this.clearAll)
  },
  beforeDestroy(){
    this.$bus.$off('deleteList')
    this.$bus.$off('addTask')
    this.$bus.$off('change')
    this.$bus.$off('clearAll')
  }
}
</script>

<style >

body {
  background: #fff;
}
#app{
  width:576px;
  margin:0 auto;
}
.btn {
  display: inline-block;
  padding: 4px 12px;
  margin-bottom: 0;
  font-size: 14px;
  line-height: 20px;
  text-align: center;
  vertical-align: middle;
  cursor: pointer;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.05);
  border-radius: 4px;
}

.btn-danger {
  color: #fff;
  background-color: #da4f49;
  border: 1px solid #bd362f;
}

.btn-danger:hover {
  color: #fff;
  background-color: #bd362f;
}

.btn:focus {
  outline: none;
}

.todo-container {
  width: 600px;
  margin: 0 auto;
}
.todo-container .todo-wrap {
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
}
</style>
