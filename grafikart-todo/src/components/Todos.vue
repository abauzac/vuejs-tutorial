<template type="html">

<section  class="todoapp">
    <header class="header">
        <h1>Todos</h1>
        <input type="text" class="new-todo" placeholder="Ajouter" v-model="newTodo" @keyup.enter="addTodo"
        >
    </header>
    <div class="main">
        <ul class="todo-list">
            <li class="todo" v-for="todo in todos" :class="{completed : todo.completed}">
                <div class="view">
                    <input type="checkbox" class="toggle__input" v-model="todo.completed"  :id="todo.labelid">
                    <label class="toggle" :for="todo.labelid"></label>
                    <div class="label">{{ todo.name }}</div>
                </div>
            </li>
        </ul>
    </div>
    <footer class="footer">
        <span class="todo-count"><strong>{{ remaining }}</strong> taches a faire</span>
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
 // 13 min 14sec
  data () {
    return {
      todos: [{
                name: 'test',
                completed: false,
                labelid : newID()
            }],
            newTodo: ''
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
        
    },
    computed: {
        remaining(){
            return this.todos.filter(todo => !todo.completed).length
        }
    }
}

</script>

<style src="./todo.css"></style>
