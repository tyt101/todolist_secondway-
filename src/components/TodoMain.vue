<template>
<ul class="todo-main">
    <TodoList :li="li" v-for="li in list" :key="li.id" ></TodoList>
</ul>
</template>

<script>
import TodoList from './TodoList'
export default {
    name:'todo-main',
    components:{
        TodoList
    },
    props:['list']
}
</script>

<style scoped>
.todo-main {
  margin-left: 0px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding: 0px;
}

.todo-empty {
  height: 40px;
  line-height: 40px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding-left: 5px;
  margin-top: 10px;
}
</style>