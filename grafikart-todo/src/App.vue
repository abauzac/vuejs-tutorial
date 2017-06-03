<template>
  <div>
    {{todos}}
    <todos v-model="todos"></todos>
    <button @click="addTodo">Ajouter tache</button>
  </div>
</template>

<script>
  import Todos from './components/Todos'

  export default {
    name: 'app',
    data () {
      return {
        todos: [{
          name: 'test',
          completed: false
        }]
      }
    },
    methods: {
      addTodo () {
        this.todos.push({
          name: 'coucou',
          completed: false
        })
      }
    },
    components: {
      Todos
    }
  }
</script>

<style>
  
</style>
