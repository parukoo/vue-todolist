<template>
  <div class="todolist-wrapper">
    <ul class="todolist">
      <li v-for="todo in filteredTodos"
        class="todoitem"
        :class="{done: todo.completed}"
        :key="todo.id">
        <todo-item
          :todo="todo"
          @done="done"
          @remove-todo="removeTodo"></todo-item>
      </li>
    </ul>
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

<style scoped>
</style>
