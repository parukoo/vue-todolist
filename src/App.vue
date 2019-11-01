<template>
  <div id="app">
  <header class="header">
    <div class="header-title-wrapper">
      <img class="header-icon" src="@/assets/img/title-icon.svg" alt="">
      <h1 class="header-title">ねこりすと</h1>
    </div>
  </header>
  <main class="site-width">
    <todo-search></todo-search>

    <todo-option
      :all-done="allDone"
      @all-done="onAllDone"
      @change-completed="changeCompleted"
      @remove-completed="removeCompleted"></todo-option>

    <todo-list 
      :todos="todos"
			:filtered-todos="filteredTodos"
			@remove-todo="removeTodo"
			@done="done">
    </todo-list>
    
    <todo-creater @add-todo="addTodo"></todo-creater>
  </main>

  <footer class="footer">
    <footer-menu 
    :visibility="visibility"
    :todos="todos"></footer-menu>
  </footer>
  </div>
</template>

<script>
import TodoSearch from './components/TodoSearch.vue';
import TodoList from './components/TodoList.vue';
import TodoCreater from './components/TodoCreater.vue';
import TodoOption from './components/TodoOption.vue';
import FooterMenu from './components/FooterMenu.vue';

var STORAGE_KEY = 'neko-list'
var todoStorage = {
  fetch: function() {
    var todos = JSON.parse(
      localStorage.getItem(STORAGE_KEY) || '[]'
    )
    todos.forEach(function(todo, index) {
      todo.id = index
    })
    todoStorage.number = todos.length
    return todos
  },
  save: function(todos) {
    localStorage.setItem(STORAGE_KEY, JSON.stringify(todos))
  }
}

const filters = {
  all(todos) {
    return todos;
  },
  active(todos) {
    return todos.filter(todo => !todo.completed);
  },
  completed(todos) {
    return todos.filter(todo => todo.completed);
  }
};
export default {
  name: 'app',
  components: {
    TodoSearch,
    TodoList,
    TodoCreater,
    TodoOption,
    FooterMenu
  },
  data(){
    return{
      todos: todoStorage.fetch(),
      number: 0,
      visibility: 'all'
    }
  },
  watch:{
    todos:{
      handler(todos){
        todoStorage.save(todos);
      },
      deep: true
    }
  },
	computed: {
    filteredTodos() {
			return filters[this.visibility](this.todos);
    },
    allDone:{
      get(){
        return this.remaining === 0;
      },
      set(value){
        this.todos.forEach((todo) =>
          todo.completed = value
        );
      }
    },
    remaining(){
      const todos = filters.active(this.todos);
      return todos.length;
    }
  },
  mounted(){
    window.addEventListener('hashchange', this.onHashChange);
  },
	methods: {
		addTodo(todoTitle) {
			const newTodo = todoTitle && todoTitle.trim();
			if (!newTodo) {
				return;
			}
			this.todos.push({
				id: todoStorage.number++,
				title: newTodo,
				completed: false
      });
      todoStorage.save(this.todos);
		},
		removeTodo(todo) {
      this.todos = this.todos.filter(item => item !== todo);
      todoStorage.save(this.todos);
		},
		done(todo, completed) {
			todo.completed = completed;
    },
    onHashChange(){
      const visibility = window.location.hash.replace(/#\/?/, '');
			this.visibility = visibility;
    },
    onAllDone(done){
      this.allDone = done;
    },
    changeCompleted(){
      this.todos.forEach((todo) =>
        todo.completed = false
      );
    },
    removeCompleted(){
      this.todos = filters.active(this.todos);
    }
	}
}
</script>

<style>
@import "./assets/css/style.css";
</style>
