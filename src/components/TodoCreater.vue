<template>
  <div class="todoCreater-wrapper">
    <input 
      type="text" 
      class="todoCreater-input" 
      :class="{active: opened}"
      placeholder="入力してくれにゃ"
      v-model="newTodo"
      @keydown.enter="addTodo">
    <img 
      class="todoCreater-icon" 
      src="@/assets/img/create-icon.svg" 
      @click="opened=!opened">
  </div>
</template>

<script>
export default {
  name: 'TodoCreater',
  components:{

  },
  props:{

  },
  data(){
    return{
      opened: false,
      newTodo: ''
    }
  },
  methods:{
    addTodo(){
      console.log('add1');
      this.$emit('add-todo', this.newTodo);
      this.newTodo = "";
    }
  }
}
</script>

