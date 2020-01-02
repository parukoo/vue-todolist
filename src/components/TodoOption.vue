<template>
  <div class="option-wrapper" v-cloak>
    <span class="option-link">
      <a 
        class="option-btn" 
        :value="allDone" 
        @click.stop="onAllDone">全選択</a>｜
      <a 
        @click.stop="changeCompleted"
        >選択解除</a>
    </span>
    <button type="button" class="delete-btn" @click="removeCompleted">削除</button>
  </div>
</template>

<script>
export default {
  name: 'TodoOption',
  components:{

  },
  props:{
    allDone: Boolean
  },
  data(){
    return{
    }
  },
  methods:{
    onAllDone(){
      console.log('alldone');
      this.$emit('all-done', !this.allDone);
    },
    changeCompleted(){
      this.$emit('change-completed');
    },
    removeCompleted(){
      this.$emit('remove-completed');
    }
  }
}
</script>

