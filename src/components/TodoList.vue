<template>
  <div class="todolist-wrapper" v-cloak>
    <transition-group 
      class="todolist" name="todoitem" tag="ul"
      leave-active-class="animated rollOut">
      <li v-for="todo in filteredTodos"
        class="todoitem"
        :class="{done: todo.completed}"
        :key="todo.id">
        <todo-item
          :todo="todo"
          @done="done"
          @remove-todo="removeTodo"></todo-item>
      </li>
    </transition-group>
  </div>
</template>

<script>
import TodoItem from './TodoItem.vue';
export default {
  name: 'TodoList',
  components:{
    TodoItem
  },
	props: {
		todos: Array,
		filteredTodos: Array
  },
	methods: {
		removeTodo(todo) {
			this.$emit('remove-todo', todo);
		},
		done(todo, completed) {
			this.$emit('done', todo, completed);
    }
	}
}
</script>

<style>


</style>
