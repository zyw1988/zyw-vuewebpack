<template>
    <div>
        <header class="header">
            <h1>康康孩子叭</h1>
            <input 
                class="new-todo" 
                placeholder="What needs to be done?" 
                autofocus
                @blur="addNewTodo($event)">
        </header>
    </div>
</template>

<script>
export default {
    props:["todoLists"],
    data(){
        return{

        }
    },
    methods:{
        addNewTodo(e){
            var todoText = e.target.value.trim();
            
            if(!todoText.length) return;
            var newTodo = {
                id:this.todoLists.length +1,
                todo_title: todoText,
                todo_isCompleted:false
            }
            this.$emit('func1',newTodo);
        }
    }
}
</script>
<style scoped>
    .header h1{
        color:rgb(194, 224, 83);
        font-family:Verdana, Geneva, Tahoma, sans-serif
    }
</style>

