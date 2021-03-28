<template>
    <div class="conatiner"> 
      <div class="addTaskCont"> 
       <AddTask @add-task="addTask" class="addTask"/>
      </div >
      <div class="tasks">
      <Tasks ref="tasks" @changeCompleted="changeCompleted" @changeProgress="changeProgress" :tasks="tasksToGive" />
      </div>
    </div>
</template>

<script>
import AddTask from './AddTask';
import Tasks from './Tasks';

export default {
  name: 'TaskContainer',
  components: {
   AddTask,
   Tasks
  },
  data(){
    return{
      tasksToGive: []
    }
  },
  props:{
      tasks: Array,
  },
  methods: {

    addTask(newTaskDatas){
      this.$emit('add-task', newTaskDatas)
    },
    changeCompleted(id){
      this.tasksToGive = this.tasks.filter((task) => task.id !== id )
      this.$emit('change-completed', id);
    },
     changeProgress(id){
      this.tasksToGive = this.tasks.map((task) => task.id === id ? {...task, inProgress: !task.inProgress} : task)
      this.$emit('change-progress', id);
    },
    setTaskToGive(tasks){
      this.tasksToGive = tasks;
      tasks += 1;
    }
  },
  created() {
    this.tasksToGive = this.tasks;
  },
  emits:['changeCompleted', 'changeProgress', 'add-task']
  }
  
</script>

<style scoped>
.conatiner {
  display: grid;
  grid-template-columns: 1fr;
  grid-template-rows: 1fr 2fr;
}

.addTask{
  background: #F3F3F3;
  margin: 1em auto;
  width: 50%;
  padding: 1em;
  border-radius: 25px; 
  box-shadow: 2px 2px 2px #C2BFBF;
}
.addTaskCont{
  border-bottom:1px solid black;
}

.tasks{
  overflow:auto;
}





</style>