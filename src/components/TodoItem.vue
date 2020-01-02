<template>
  <div class="todoitem-wrapper">
    <img class="todoitem-check" src="@/assets/img/icon-check.svg" alt="" @click="onInput">
    <img class="todoitem-check-done animated shake" src="@/assets/img/icon-check-done.svg" alt="" @click="onInput">    
    <span 
      @dblclick="edit=!edit"
      :class="{display: !edit}"
      class="todoitem-txt"><span class="border">{{todo.title}}</span></span>
    <input
      v-model="todo.title"
      :class="{display: edit}" 
      type="text" class="todoitem-input"
      @keypress.enter="edit=!edit"
      @blur="edit=!edit">
    <v-fa @click="removeTodo" class="todoitem-trash" :icon="['far', 'trash-alt']" />
  </div>
</template>

<script>

export default {
  name: 'TodoItem',
  props:{
    todo: Object,
  },
  data(){
    return{
      edit: false,
    }
  },
	methods: {
		removeTodo() {
			this.$emit('remove-todo', this.todo);
		},
		onInput() {
      console.log('done1');
			this.$emit('done', this.todo, !this.todo.completed);
    }
	}
}
</script>

<style>
.todoitem-wrapper{
  position: relative;
  margin-bottom: 20px;
}
.todoitem-check-done{
  display: none;
  position: absolute;
  left: 12px;
  top: 12px;
  cursor: pointer;
  z-index: 1;
}
.todoitem.done .todoitem-check-done{
  display: block;
  opacity: 0.5;
}
.todoitem.done .todoitem-check{
  display: none;
}
.todoitem.done .border{
  display: inline-block;
  position: relative;
}
.todoitem.done .border::before{
  content: '';
  display: inline-block;
  width: 100%;
  height: 2px;
  background-color: #333;
  position: absolute;
  top: 11px;
}
.todoitem-input.display{
  display: block;
}

</style>
