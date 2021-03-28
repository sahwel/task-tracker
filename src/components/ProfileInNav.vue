<template>
    <div class="container"> 
         <img class="profile-pic" src="@/assets/profilePic.jpg">
        <div class="name-icon">
            <p>{{username}}</p>
            <img class="arrow" src="@/assets/Vector.png">
        </div>
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
.container {
    display: grid;
    padding: 0.5em;
    border-bottom: 1px solid black;
    grid-template-columns: 1fr 4fr;
}
.name-icon{
    display: grid;
    grid-template-columns: 1fr 2fr;
}


.profile-pic{
    width: 2.5em;
    height: 3em;
}
.arrow{
    padding: 0.5em;
    width: 0.8em;
    height:0.5em;
    margin: auto 0;
}
.arrow:hover{
    background: #D8D8D8;
    border-radius: 50%;
}

p{
    font-size: 1.2em;
    margin: auto 0;
}
</style>