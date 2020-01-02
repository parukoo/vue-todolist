<template>
  <div class="search-wrapper" >
    <input 
      type="text" 
      class="search-input"
      :value="value"
      placeholder="検索するぞ！"
      @input="searchTodo">
  </div>
</template>

<script>
export default {
  name: 'TodoSearch',
  components:{

  },
  data(){
    return{
    }
  },
  props: ['value'],
  methods:{
    searchTodo(e){
      console.log(event.target.value);
      this.$emit('input', e.target.value);
    }
  }
}
</script>

