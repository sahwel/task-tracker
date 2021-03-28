<template>
    <div class="conatiner"> 
    
    <NavComponent class="NavComponent" name="Not completed tasks" :howMuch="nonCompletedTasksSize" /> 
    <NavComponent class="NavComponent" name="In progress" :howMuch="inProgressTasksSize" />
    <NavComponent class="NavComponent" name="Not in progress" :howMuch="notInProgressTasksSize" />
    <NavComponent class="NavComponent" name="Completed" :howMuch="completedTasksSize" />
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
.conatiner {
}

.NavComponent{
  width: 80%;
  margin: 0 auto;
}
</style>