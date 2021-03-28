<template>
    <div class="conatiner"> 
      <div class="addTaskCont"> 
       <AddTask @add-task="asd" class="addTask"/>
      </div >
      <div class="tasks">
      <Tasks @changeCompleted="changeCompleted" @changeProgress="changeProgress" :tasks="nonCompletedTasks" />
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
    return {
      nonCompletedTasks: []
    }
  },
  props:{
      tasks: Array,
  },
  methods: {
    asd(newTaskDatas){
      console.log(newTaskDatas)
      this.$emit('add-task', newTaskDatas)
    },
    changeCompleted(id){
      this.nonCompletedTasks = this.nonCompletedTasks.filter((task) => task.id !== id )
      this.$emit('change-completed', id);
    },
     changeProgress(id){
      this.nonCompletedTasks = this.nonCompletedTasks.map((task) => task.id === id ? {...task, inProgress: !task.inProgress} : task)
      this.$emit('change-progress', id);
    }
  },
  created(){
    this.nonCompletedTasks = this.tasks.filter((task) => task.completed === false);
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