<template>
  <ul class="footer-menus">
    <li class="footer-menu" :class="{selected: visibility === 'all'}">
      <a href="#/all">
        <div class="footer-icon-wrapper">
          <img src="@/assets/img/title-icon.svg" alt="" class="footer-menu-icon">
          <span class="footer-menu-name">ALL</span>
        </div>
      </a>
    </li>
    <li class="footer-menu" :class="{selected: visibility === 'active'}">
      <a href="#/active">
        <div class="footer-icon-wrapper">
          <img src="@/assets/img/incomplete-icon.svg" alt="" class="footer-menu-icon">
          <span class="footer-menu-name">未完了</span>
        </div>
      </a>
    </li>
    <li class="footer-menu" :class="{selected: visibility === 'completed'}">
      <a href="#/completed">
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
  props:{
    todos: Array,
    visibility: String
  },
  data(){
    return{
    }
  }
}
</script>

