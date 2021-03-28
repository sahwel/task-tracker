<template>
    <div class="container"> 
        <img class="arrow" src="@/assets/mi_log-out.png">
        <p>Log out</p>
    </div>
</template>

<script>
export default {
  name: 'Logout'
  
}
</script>


<style scoped>
.container{
    position: relative;
    display: grid;
    grid-template-columns: 1fr 3fr;  
}
img{
    margin: auto 0.5em 0.5em 1em;
    width: 2em;
}

p{
    -webkit-user-select:none;
    -moz-user-select:none;
    user-select:none;
    margin: auto 0;
    font-size: 1.1em;
}

</style>