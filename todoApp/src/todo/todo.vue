<template>
  <section class="real-app">
        <input 
            type="text"
            class="add-input"
            autofocus="autofocus"
            placeholder="What to do?"
            @keyup.enter="addTodo"  
        >
        <Item 
            :todo="todo"
            v-for="todo in filteredTodos"
            :key="todo.id"
            @del="deleteTodo"
        />
        <Tabs 
            :filter="filter" 
            :todos="todos"
            @toggle="toggleFilter"
            @clearAllCompleted="clearAllCompleted"
        />
  </section>
</template>

<script>
import Item from './item.vue'
import Tabs from './tabs.vue'
let id = 0
export default {
  data() {
      return {
          todos: [],
          filter: 'all'
      }
  },
  components: {
      Item,
      Tabs
  },
  computed: {
      filteredTodos(){
          if(this.filter === 'all'){
              return this.todos
          }
          const completed = this.filter === 'completed'
          return this.todos.filter(todo => completed === todo.completed) 
      }
  },
  methods: {
      addTodo(e){
          this.todos.unshift({
              id: id++,
              content: e.target.value.trim(),
              completed: false
          })
          e.target.value = ''
      },
      deleteTodo(id){
          this.todos.splice(this.todos.findIndex(todo => todo.id === id), 1)
      },
      toggleFilter(state){
          this.filter = state
      },
      clearAllCompleted(){
          this.todos = this.todos.filter(todo => !todo.completed)
      }
  }
}
</script>

<style lang="stylus" scoped>
    .real-app{
        position relative
        width 600px
        margin 0 auto 
        box-shadow 0 0 5px #666
    }
    .add-input{
        position relative
        display block
        margin 0 auto
        width 86%
        font-size 24px
        outline none
        font-family inherit 
        font-weight inherit
        line-height 1.4em
        padding 16px 4% 16px 10%
        border 0px
        border-bottom 1px solid black
    }
</style>

