<template>
    <div class="w-full flex">
        <div class="m-auto flex flex-col items-center  h-screen">
        <h1 class="text-4xl text-center my-5">To Do List</h1>
        <div class="text-2xl text-center italic my-5">{{ today() }}</div>
        <h2 class="text-2xl text center mb-5"> {{ todosCount }} tasks</h2>

        <ul>
            <li class="flex justify-between m-3" v-for="(todo, index) in todos" :key="todo.task">
            <div>
                {{ todo.task }} 
            </div>
            <button class="mx-5" @click="remove(index)">x</button>
            </li>
        </ul>
        <form class="mt-10" @submit.prevent="addHero">
            <input class="border rounded-lg p-1" v-model="newTodo" placeholder="Add a Task"/>
            <button class="border rounded bg-gradient-to-r from-blue-700 to-blue-300 text-sm text-white p-1" type="submit"> Add Task</button>
        </form>
        </div>
    </div>
</template>

<script>
import today from '../utilities/mixins/today';
export default {
    mixins: [today],
    computed: {
        todosCount() {
            return this.todos.length
        },
    },
    methods:{
        addHero(){
        if(this.newTodo !== "") {
            this.todos.push({name:this.newTodo})
            this.newTodo = "";
        }
        },
        remove(index) {
        this.todos = this.todos.filter((todo, i) => i !== index);
        }
    },
    data() {
        return {
            newTodo:'',
            todos: [
                {task: "Hacker Rank"},
                {task: "Code Wars"},
                {task: "Job Applications" },
                {task: "Vue JS" },
                {task: "Study Computer Science" }
            ]
        }
    }
}
</script>