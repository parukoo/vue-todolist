<template>
  <ul class="footer-menus">
    <li class="footer-menu">
      <a href="#/all" :class="{selected: visibility === 'all'}">
        <div class="footer-icon-wrapper">
          <img src="@/assets/img/title-icon.svg" alt="" class="footer-menu-icon">
          <span class="footer-menu-name">ALL</span>
        </div>
      </a>
    </li>
    <li class="footer-menu">
      <a href="#/active" :class="{selected: visibility === 'active'}">
        <div class="footer-icon-wrapper">
          <img src="@/assets/img/incomplete-icon.svg" alt="" class="footer-menu-icon">
          <span class="footer-menu-name">未完了</span>
        </div>
      </a>
    </li>
    <li class="footer-menu">
      <a href="#/completed" :class="{selected: visibility === 'completed'}">
        <div class="footer-icon-wrapper">
          <img src="@/assets/img/complete-icon.svg" alt="" class="footer-menu-icon">
          <span class="footer-menu-name">完了</span>
        </div>
      </a>
    </li>
  </ul>
</template>

<script>
export default {
  name: 'FooterMenu',
  components:{

  },
  data(){
    return{
      todos: Array,
      visibility: String
    }
  }
}
</script>

<style scoped>
.footer-menu a{
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center; 
}
.footer-menu.selected{
  opacity: 0.8;
}
</style>
