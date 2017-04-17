<template type="html">
    <section  class="todoapp">
        <header class="header">
            <h1>Todos</h1>
            <input type="text" class="new-todo" placeholder="Ajouter" v-model="newTodo" @keyup.enter="addTodo"
            >
        </header>
        <div class="main">
            <input type="checkbox" class="toggle-all" v-model="allDone">
            <ul class="todo-list">
                <li class="todo" v-for="todo in filteredTodos" :class="{completed : todo.completed}">
                    <div class="view">
                        <input type="checkbox" class="toggle__input" v-model="todo.completed"  :id="todo.labelid">
                        <label class="toggle" :for="todo.labelid"></label>
                        <div class="label">{{ todo.name }}</div>
                        <button class="destroy" @click.prevent="deleteTodo(todo)"></button>
                    </div>
                </li>
            </ul>
        </div>
        <footer class="footer" v-show="todos.length > 0">
            <span class="todo-count"><strong>{{ remaining }}</strong> taches a faire</span>
            <ul class="filters">
                <li>
                    <a href="#" :class="{selected : filter === 'all'}" @click.prevent="filter = 'all'">Toutes </a>
                </li>
                <li>
                    <a href="#" :class="{selected : filter === 'todo'}" @click.prevent="filter = 'todo'">A faire </a>
                </li>
                <li>
                    <a href="#" :class="{selected : filter === 'done'}" @click.prevent="filter = 'done'">Faites </a>
                </li>
            </ul>
            <button class="clear-completed" v-show="completed" @click.prevent="deleteCompleted">Supprimer taches finies</button>
        </footer>
    </section>
</template>

<script>
/* eslint-disable */
var labelid = 0;
function newID(){
    return "id-" + labelid++;
}

export default {
 // 18 min 14sec
  data () {
    return {
        
        todos: [{
                    name: 'test',
                    completed: false,
                    labelid : newID()
                }],
                newTodo: '',
                filter: 'all'
            }
    },
    methods: {
        addTodo(){
            this.todos.push({
                completed:false,
                name: this.newTodo,
                labelid : newID()
            })
            this.newTodo = '';
        },
        deleteTodo(todo){
            this.todos = this.todos.filter(key => key !== todo)
        },
        deleteCompleted(){
            this.todos = this.todos.filter(key => !key.completed)
        },
        
    },
    computed: {
        allDone : {
            get(){
                return this.remaining === 0
            },
            set(value){
                this.todos.forEach(function(todo) {
                    todo.completed = value;
                }, this);
            }
        },
        remaining(){
            return this.todos.filter(todo => !todo.completed).length
        },
        completed(){
            return this.todos.filter(todo => todo.completed).length != 0;
        },
        filteredTodos (){
            if(this.filter == 'todo'){
                return this.todos.filter(todo => !todo.completed)
            }
            else if(this.filter == 'done'){
                this.todos.filter(todo => todo.completed)
            }
            return this.todos;
        }
    }
}

</script>

<style src="./todo.css"></style>
