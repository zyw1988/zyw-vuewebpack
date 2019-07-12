<template>
    <div>
        <section class="main">
            <input id="toggle-all" class="toggle-all" type="checkbox" v-model="ToggleAll">
            <label for="toggle-all" 
                >Mark all as complete</label>
            <ul class="todo-list">
                <li v-for="(item,index) in con_todoLists" 
                    :key="item.id"
                    :class="{
                        editing:editIndex==index,
                        completed:item.todo_isCompleted==true}">
                    <div class="view">
                        <input 
                            class="toggle" type="checkbox" 
                            v-model="item.todo_isCompleted"
                          >
                        <label 
                            @dblclick="dbCLickEdit(index)"
                            >{{ item.todo_title }}</label>
                        <button 
                            class="destroy"
                            @click="deleteTodo(index)"></button>
                    </div>
                    <!-- 进入修改状态的input，增加 修改-保存 和修改-放弃事件 -->
                    <input class="edit" 
                            :value="item.todo_title"
                            @blur="saveChangeNewTodo($event,index)"
                            @keyup.enter="saveChangeNewTodo($event,index)"
                            @keyup.esc="abandonChangeNewTodo">
                </li>
            </ul>
        </section>
			
        <footer class="footer" v-if="con_todoLists.length">
            
            <span class="todo-count"><strong>{{ con_todoLists.filter(item=>!item.todo_isCompleted).length}}</strong> item left</span>
            
            <ul class="filters">
                <li>
                    <a class="selected" href="#/">All</a>
                </li>
                <li>
                    <a href="#/active">Active</a>
                </li>
                <li>
                    <a href="#/completed">Completed</a>
                </li>
            </ul>
            <!-- Hidden if no completed items are left ↓ -->
            <button 
                class="clear-completed"
                @click="deleteAllCompleted">Clear completed</button>
        </footer>
    </div>
</template>
<script>
window.onhashchange = function(){
   var hashText = this.location.hash.substring(2);
//    hashText= hashText==""?"all":hashText;
//    console.log(hashText)
    this.hashName = hashText;
}
export default {
    props:["todoLists"],
    data() {
        return {
            con_todoLists:this.todoLists,
            editIndex:null,
            selectedText:"",
            hashName:"all"
        }
    },
    watch:{
        "hashName":function(){
            console.log(2222)
        }
    },
    computed:{
        ToggleAll:{
            set:function(){
                var bool =!this.ToggleAll
                for(var i = 0; i <this.con_todoLists.length;i ++){
                    this.con_todoLists[i].todo_isCompleted = bool;
                } 
            },
            get:function(){
                return this.con_todoLists.every(item=>item.todo_isCompleted)
            }
        }
    },
    methods:{
        // show(){console.log(999)},
        deleteTodo(index){
            this.$emit('func2',index);
        },
        dbCLickEdit(index){
           this.editIndex = index;
            // console.log(index)
        },
        // 保存修改的tudo
        saveChangeNewTodo(e,index){
            var todoText = e.target.value;
            // console.log('修改了已保存')
            // console.log(todoText,index)
            this.$emit("func3",todoText,index);
            this.editIndex = null;
        },
        // 放弃修改八寸
        abandonChangeNewTodo(){
            // console.log('修改了并取消保存')
            this.editIndex = null;
        },
        // 清空所有completed
        deleteAllCompleted(){
            this.$emit("func4");
        }
    }
}
</script>
