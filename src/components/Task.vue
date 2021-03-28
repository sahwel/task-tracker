<template>
<div class="container"> 
    <div class="header">
        <h3>{{task.name}}</h3> 
        <h3 class="date">{{task.created}}</h3>
    </div> 
    <div class="description">
        <div class="d-text">
        {{task.description}}
             </div>
        <div class="icons">
            <img @click="$emit('changeProgress', task.id)" :src="task.inProgress ? stop : start ">
            <img @click="$emit('changeCompleted', task.id)" src="@/assets/pipa.png">
        </div>
    </div>
</div>
</template>

<script>

export default {
  name: 'Task',
  props: {
    task: Object,
  },
  data(){
      return{

      start: require('@/assets/start.png'),
      stop: require('@/assets/stop.png'),
      }
  }
}
</script>

<style scoped>
.container{
    border-radius: 25px;
    background: #F3F3F3;
    margin: 0 auto;
    margin-top: 1em;
    width: 65%;
}

.description, .header{
    display: grid;
    width: 95%;
    margin: 0 auto;
}
.header{
    grid-template-columns: 3fr 1fr;
    border-bottom: 1px solid black;
}
.date{
    justify-self: end;
}

.description{
    padding: 1em;
    grid-template-columns: 5fr 1fr;
    grid-auto-rows: minmax(4em, 4em);
    grid-auto-columns: minmax(1fr, 3fr);
}

.icons{
    
    justify-self: end;
    align-self: end;
}
.icons > img {
    padding: 0 0.2em;
    width: 1.5em;
}



.d-text{ 
   
  word-wrap: break-word;
  word-break: break-all;
}

</style>
