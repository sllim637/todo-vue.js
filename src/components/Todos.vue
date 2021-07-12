<template>
    <section class="todoapp">
         <header class="header">
            <h1>Todos</h1>
            <input type="text" class="new-todo" placeholder="ajouter une tache" v-model="newTodo" @keyup.enter="addTodo">
         </header>
         <div class="main">
  <input type="checkbox" class="toggle-all" v-model="allDone">
             <ul class="todo-list">
                 <li class="todo" v-for="todo in filteredTodo" :key="todo" :class="{completed: todo.completed, editing: todo === editing }">
                     <div class="view">
                         <input type="checkbox" class="toggle" v-model="todo.completed">
                        <label @dblclick="editTodo(todo)" >{{ todo.name }}</label>
                        <button class="destroy" @click.prevent="deleteTodo(todo)"></button>
                     </div>
                     <input type="text" class="edit" @keyup.enter="doneEdit" @blur="doneEdit" v-focus="todo === editing" @keyup.esc="cancelEdit" v-model="todo.name">
                 </li>
             </ul>
         </div>
         <footer class="footer" v-show="hasTodos()">
             <span class="todo-count"><strong>{{ remaining }}</strong> tache à faire </span>
             <ul class="filters">
                 <li> <a href="#" :class="{selected: filter ==='all' }" @click.prevent="filter='all'">Toutes</a> </li>
                 <li> <a href="#" :class="{selected: filter ==='todo' }" @click.prevent="filter='todo'" >A faire </a> </li>
                 <li> <a href="#" :class="{selected: filter ==='done' }" @click.prevent="filter='done'">Faites</a> </li>
             </ul>
             <button v-show="completed" class="clear-completed" @click.prevent="deleteCompleted">Supprimer les taches finis</button>
         </footer>
    </section>
</template>
<script>
export default{
  data () {
    return {
      todos: [{
        name: 'tache de test',
        completed: false
      }],
      newTodo: '',
      filter: 'all',
      editing: null,
      oldTodo: ''
    }
  },
  methods: {
    addTodo () {
      this.todos.push({
        completed: false,
        name: this.newTodo

      })
      this.newTodo = ''
    },
    hasTodos () {
      return this.todos.length > 0
    },
    deleteTodo (todo) {
      this.todos = this.todos.filter(i => i !== todo)
    },
    deleteCompleted () {
      // eslint-disable-next-line eqeqeq
      this.todos = this.todos.filter(i => i.completed == false)
    },
    editTodo (todo) {
      this.editing = todo
      this.oldTodo = todo.name
    },
    doneEdit () {
      this.editing = null
    },
    cancelEdit () {
      this.editing.name = this.oldTodo
      this.doneEdit()
    }

  },
  computed: {
    allDone: {
      get () {
        return this.remaining === 0
      },
      set (value) {
        this.todos.forEach(todo => {
          todo.completed = value
        })
      }
    },
    remaining () {
      return this.todos.filter(todo => !todo.completed).length
    },
    completed () {
      return this.todos.filter(todo => todo.completed).length
    },
    filteredTodo () {
      if (this.filter === 'todo') {
        return this.todos.filter(todo => !todo.completed)
      } else if (this.filter === 'done') {
        return this.todos.filter(todo => todo.completed)
      }
      return this.todos
    }
  },
  directives: {
    focus (el, value) {
      if (value) {
        el.focus()
      }
    }
  }

}
</script>
<style src="./todos.css">

</style>
