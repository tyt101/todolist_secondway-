<template>
<div class="todo-footer" v-show="getTotal">
    <label>
        <input type="checkbox" :checked="isAll" @change="changeAllTask"/>
    </label>
    <span>
        <span>已完成{{getFinished}}</span> / 全部{{getTotal}}
    </span>
    <button class="btn btn-danger"
    @click="clear()"
    >清除已完成任务</button>
</div>
</template>

<script>
export default {
    name:'todo-footer',
    props:['list'],
    data() {
        return {
            ischecked:''
        }
    },
    computed:{
        getTotal(){
            return this.list.length
        },
        getFinished(){
            return this.list.filter(task=>{
                return task.isDone
            }).length
        },
        isAll(){
            return this.getTotal===this.getFinished
        }
    },
    methods: {
        changeAllTask(e){
            this.$bus.$emit('change',e.target.checked)
            console.log(e.target.checked)
        },
        clear(){
            this.$bus.$emit('clearAll');
        }
    },
}
</script>

<style scoped>
.todo-footer {
  height: 40px;
  line-height: 40px;
  padding-left: 6px;
  margin-top: 5px;
}

.todo-footer label {
  display: inline-block;
  margin-right: 20px;
  cursor: pointer;
}

.todo-footer label input {
  position: relative;
  top: -1px;
  vertical-align: middle;
  margin-right: 5px;
}

.todo-footer button {
  float: right;
  margin-top: 5px;
}
</style>