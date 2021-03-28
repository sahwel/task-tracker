<template>
    <div class="container"> 
    <ProfileInNav class="profile" username="metramyt"/> 
    <Nav  @not-completed="$emit('not-completed')" @in-progress="$emit('in-progress')"  @not-in-progress="$emit('not-in-progress')"   @completed="$emit('completed')"  :key="navkey" :tasks="tasks" />
    <Logout class="logout" />
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


.logout{
    position: absolute;
    bottom: 0px;
}
</style>