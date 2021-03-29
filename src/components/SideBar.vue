<template>
    <div class="container"> 
      <img class="hamburger" src="@/assets/hamburger-menu.png">
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
  props:{
    tasks: Array
  },
  methods:{
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
  .desktop{
    display: none;
  }
}
</style>