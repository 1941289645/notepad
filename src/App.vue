<template>
  <!-- 主体区域 -->
  <section id="app">
    <TodoHeader @add="handleAdd"></TodoHeader>
    <TodoMain :list="list" @del="handleDel"></TodoMain>
    <TodoFooter @clear="hanldeClear" :list="list"></TodoFooter>
  </section>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoMain from './components/TodoMain.vue'
import TodoFooter from './components/TodoFooter.vue'

export default {
  data () {
    return {
      list:JSON.parse(localStorage.getItem('list'))||[
        {id:1,name:'打篮球'},
        {id:2,name:'看电影'},
        {id:3,name:'逛街'},
      ]
    }
  },
  watch:{
    list:{
      deep:true,
      handler(newVal){
        localStorage.setItem('list',JSON.stringify(newVal))
        if(this.list.length === 0){
          localStorage.removeItem('list')
        }
      }
    }
  },
  components:{
    TodoHeader,
    TodoMain ,
    TodoFooter,
  },
  methods:{
    handleAdd(todoName){
      this.list.unshift({
        id:+new Date(),
        name:todoName
      })
    },
    handleDel(id){
      // console.log(id);
      this.list = this.list.filter(item=>item.id !== id)
    },
    hanldeClear(){
      this.list = []
    }
  }
}
</script>

<style>

</style>
