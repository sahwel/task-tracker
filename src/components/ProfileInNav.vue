<template>
    <div class="conatiner"> 
    <img class="profile-pic" src="@/assets/profilePic.jpg">
    <p>{{username}}</p>
    <img class="arrow" src="@/assets/Vector.png">
    </div>
</template>

<script>
export default {
  name: 'ProfileInNav',
 
  props: {
      username: String
  }
 }
</script>

<style scoped>
.conatiner {
    display: grid;
    padding: 0.5em;
    border-bottom: 1px solid black;
    grid-template-columns: 20% auto 50%;
}
.profile-pic{
    width: 2.5em;
    height: 3em;
    margin: auto 0;
}
.arrow{
    width: 0.8em;
    height:0.5em;
    margin: auto 0;
}

p{
    font-size: 1.2em;
    margin: auto 0;
}
</style>