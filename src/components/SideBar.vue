<template>
    <div class="container"> 
      <img  :class="isNavActive ? 'hamburger' : 'hamburger'" @Click="openMobileNav"   src="@/assets/hamburger-menu.png">
      <Nav :class="isNavActive ? 'nav-in-mobile inline  ' : 'nav-in-mobile'" @not-completed="$emit('not-completed')" @in-progress="$emit('in-progress')"  @not-in-progress="$emit('not-in-progress')"   @completed="$emit('completed')"  :key="navkey" :tasks="tasks" />
      <div class="desktop">
        <ProfileInNav class="profile" username="metramyt"/> 
        <Nav  @not-completed="$emit('not-completed')" @in-progress="$emit('in-progress')"  @not-in-progress="$emit('not-in-progress')"   @completed="$emit('completed')"  :key="navkey" :tasks="tasks" />
        <Logout class="logout" />
      </div>
    </div>
</template>

<script>
import ProfileInNav from './ProfileInNav';
import Nav from './Nav';
import Logout from './Logout';
export default {
  name: 'SideBar',
  components: {
    ProfileInNav,
    Nav,
    Logout
  },
  data(){
    return{
      isNavActive: Boolean
    }
  },
  props:{
    tasks: Array
  },
  created(){
    this.isNavActive = false;
  },
  methods:{
    openMobileNav(){
      this.isNavActive = !this.isNavActive;
    },
    reRender(){
      this.navkey += 1;
    }
  },
  emits:['not-completed', 'in-progress', 'not-in-progress', 'completed']
  
}
</script>

<style scoped>
.hamburger{
  display: none;
}

.nav-in-mobile{
  display: none;
}

.logout{
    position: absolute;
    bottom: 0px;
}

@media screen and (max-width: 992px) {
  .hamburger{
  display: inline;
  width: 1.5em;
  padding: 0.5em;
  }

  .inline {
    display: inline
  }

  .desktop{
    display: none;
  }
  
}
</style>