<template>
  <div id="app">
     <section class="todoapp">
          <todo-top 
              :todoLists="todoLists"
              @func1="AppaddNewtodo"></todo-top>
          <contain 
            :todoLists="todoLists"
            @func2="AppdeleteTodo"
            @func3="AppChangeTodo"
            @func4="AppDeleteAllCompleted"></contain>
     </section>
     <todo-footrt></todo-footrt>
  </div>
</template>

<script>
import head from './components/heade'
import footer from './components/footer'
import contain from './components/contain'

export default {
  name: 'App',
  data () {
    return {
        todoLists:[
          { id:1,todo_title:"写作业",todo_isCompleted:false },
          { id:2,todo_title:"背英语单词",todo_isCompleted:false },
          { id:3,todo_title:"完成语文周记",todo_isCompleted:true },
          { id:4,todo_title:"背诵作文段落",todo_isCompleted:false }
        ],
    }
  },
  components:{
    todoTop:head,
    todoFootrt:footer,
    contain
  },
  methods:{
    // 增
    AppaddNewtodo(newtodo){
      this.todoLists.push(newtodo)
    },
    // 删
    AppdeleteTodo(index){
      this.todoLists.splice(index,1);
    },
    // 改,传过来新的值和所引致
    AppChangeTodo(newTodoText,Todoindex){
      // console.log('收到了哦',newTodoText,Todoindex)
     /*  var temp = this.todoLists.findIndex(function(item,index){
        return index==Todoindex;
      })
      console.log(temp) */
      for(var i =0;i <this.todoLists.length;i++){
        if(i==Todoindex){
          this.todoLists[i].todo_title = newTodoText
        }
      }
    },
    // 删除所有完成的
    AppDeleteAllCompleted(){
      for(var i = this.todoLists.length-1; i >=0;i--){
        if(this.todoLists[i].todo_isCompleted==true){
          this.todoLists.splice(i,1);
        }
      }
    }
  }
}
</script>

<style>

</style>
