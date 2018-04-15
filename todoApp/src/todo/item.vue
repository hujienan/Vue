<template>
  <div :class="['todo-item', todo.completed ? 'completed' : '']">
      <input 
        type="checkbox"
        class="toggle"
        v-model="todo.completed"
      >
      <label>{{ todo.content }}</label>
      <button class="destroy" @click="deleteTodo"></button>
  </div>
</template>

<script>
export default {
  props: {
      todo: {
          type: Object,
          required: true,
      }
  },
  methods: {
      deleteTodo(){
          this.$emit('del', this.todo.id)
      }
  }
}
</script>

<style lang="stylus" scoped>
    .todo-item{
        position relative
        padding 15px 0;
        background-color #fff   
        font-size 24px
        width 100%
        border-bottom 1px solid black
        label {
            white-space pre-line
            word-break break-all
            padding 15px 60px 15px 15px
            margin-left 45px
            display block 
            line-height 1.2
            transition color 0.4s ease-out
        }
        &:hover{
            .destroy:after{
                content 'x'
            }
        }
        &.completed{
            label{
                color #d9d9d9
                text-decoration line-through
            }
        }  
    }
    
    .toggle{
        text-align center
        line-height 40px
        outline none 
        border none 
        appearance none
        height 40px
        width 40px
        position absolute 
        top 0
        left 5px
        bottom 0
        margin auto 0
        &:after{
            content url('../assets/images/round.svg')
        }
        &:checked:after{
            content url('../assets/images/done.svg')
        } 
    }
    .destroy{
        text-align center
        line-height 40px
        position absolute
        top 0
        right 10px
        bottom 0
        width 40px
        height 40px
        margin auto 0
        font-size 30px
        color grey 
        background-color transparent
        appearance none 
        border none 
        outline none
    }
</style>
