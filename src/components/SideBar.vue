<template>
    <div class="conatiner"> 
    <ProfileInNav username="metramyt"/> 
    <Nav :tasks="tasks" />
    </div>
</template>

<script>
import ProfileInNav from './ProfileInNav';
import Nav from './Nav';
export default {
  name: 'SideBar',
  components: {
    ProfileInNav,
    Nav
  },
  props:{
    tasks: Array
  }
  
}
</script>

<style scoped>
.conatiner {
}

</style>