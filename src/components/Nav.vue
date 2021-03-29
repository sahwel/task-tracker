<template>
    <div class="container"> 
    <NavComponent @Click="$emit('not-completed')" class="NavComponent" name="Not completed tasks" :howMuch="nonCompletedTasksSize" /> 
    <NavComponent @Click="$emit('in-progress')" class="NavComponent" name="In progress" :howMuch="inProgressTasksSize" />
    <NavComponent @Click="$emit('not-in-progress')" class="NavComponent" name="Not in progress" :howMuch="notInProgressTasksSize" />
    <NavComponent @Click="$emit('completed')" class="NavComponent" name="Completed" :howMuch="completedTasksSize" />
    </div>
</template>

<script>
import NavComponent from './NavComponent';
export default {
    name: 'Nav',
    components: {
        NavComponent
    },
    props:{
        tasks: Array
    },
    data(){
        return{
            completedTasksSize: Number,
            nonCompletedTasksSize: Number,
            inProgressTasksSize: Number,
            notInProgressTasksSize: Number,
        }
    },
    created(){
        this.completedTasksSize = this.tasks.filter((task) => task.completed === true).length;
        this.nonCompletedTasksSize = this.tasks.filter((task) => task.completed === false).length;
        
        this.inProgressTasksSize =this.tasks.filter((task) => task.completed === false).filter((task) => task.inProgress === true).length;
        this.notInProgressTasksSize = this.tasks.filter((task) => task.completed === false).filter((task) => task.inProgress === false).length;
  },
  
}
</script>

<style scoped>

.NavComponent{
  width: 80%;
  margin: 0 auto;
}

@media screen and (max-width: 1300px) {
   .NavComponent{
  width: 100%;
}

.NavComponent:first-child{
    
    border-top: 1px solid black;
}
}
</style>