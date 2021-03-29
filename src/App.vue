<template>
  <SideBar @not-completed="notCompleted"  @completed="completed"  @not-in-progress="notInProgress"  @in-progress="isInProgress"  ref="sideBar" :key="sideBar" :tasks="tasks" class="SideBar"/>
  <TaskContainer  ref="taskc" :key="TaskContainer"  @add-task="addTask"  @change-completed="changeCompleted" @change-progress="changePprogress" :tasks="tasks" class="taskContainer"/>
</template>

<script>
import SideBar from './components/SideBar'
import TaskContainer from './components/TaskContainer'

export default {
  name: 'App',
  components: {
    SideBar,
    TaskContainer
  },
  data(){
    return {
      tasks: [],
    }
  },
  methods:{
    
    notCompleted(){
        this.$refs.taskc.setTaskToGive(this.tasks.filter((task) => task.completed === false));
    },
    completed(){
       this.$refs.taskc.setTaskToGive(this.tasks.filter((task) => task.completed === true));
    },
    isInProgress(){
      this.$refs.taskc.setTaskToGive(this.tasks.filter((task) => task.inProgress === true));
    },
    notInProgress(){
      this.$refs.taskc.setTaskToGive(this.tasks.filter((task) => task.inProgress === false).filter((task) => task.completed !== true));
    },
    addTask(newTaskDatas){
      const defMonth = newTaskDatas.created.getMonth() +1 
      const  month=  defMonth < 11 ? '0' + defMonth : defMonth; 
      const createDate = newTaskDatas.created.getFullYear() + '-'  + month + '-' + newTaskDatas.created.getDate();
      let idd = 1;
      if( this.tasks.length !== 0 ){
        idd =  this.tasks[this.tasks.length - 1].id + 1
      }
      const newTask = {
        id: idd,
        name: newTaskDatas.name,
        description: newTaskDatas.description,
        created: createDate,
        inProgress: false,
        completed: false
      }
      this.tasks = [...this.tasks ,newTask];
      this.$refs.taskc.setTaskToGive(this.tasks.filter((task) => task.completed === false));
    },
    changeCompleted(id){
      this.tasks = this.tasks.map((task) => task.id === id ? {...task, completed: !task.completed} : task);
      this.tasks = this.tasks.map((task) => task.id === id ? {...task, inProgress: false} : task);
      this.$refs.taskc.setTaskToGive(this.tasks.filter((task) => task.completed === false));
      this.$refs.sideBar.reRender();
    },
    changePprogress(id){
      this.tasks = this.tasks.map((task) => task.id === id ? {...task, inProgress: !task.inProgress} : task);
      this.$refs.taskc.setTaskToGive(this.tasks.filter((task) => task.completed === false));
      this.$refs.sideBar.reRender();
    }
  },
  created(){
    this.tasks = [
     
    ];
     this.tasks = this.tasks.filter((task) => task.completed === false);
  },
  
  emits:['change-completed', 'change-progress', 'add-task', 'not-completed', 'in-progress', 'not-in-progress', 'completed']
}
</script>

<style>
html, body{
  margin: 0;
  padding: 0;
  height: 100vh;
  overflow-y: hidden;
}
#app {
  display: grid;
  grid-template-columns: 1fr 6fr;
}

.SideBar{
  border-right:1px solid black;
  height: 100vh;
}


.taskContainer{
  height: 100vh;
}


@media screen and (max-width: 992px) {
  #app {
 display: grid;
  grid-template-columns: 1fr;
 }
 .SideBar{
  height: auto;
}

}
</style>
