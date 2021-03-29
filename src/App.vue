<template>
  <SideBar @not-completed="notCompleted"  @completed="completed"  @not-in-progress="notInProgress"  @in-progress="isInProgress"  ref="sideBar" :key="sideBar" :tasks="tasks" class="SideBar"/>
  <TaskContainer  ref="taskc" :key="TaskContainer"  @add-task="addTask"  @change-completed="changeCompleted" @change-progress="changeProgress" :tasks="tasks" class="taskContainer"/>
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
    async addTask(newTaskDatas){
      console.log('asd')
      const defMonth = newTaskDatas.created.getMonth() +1 
      const  month=  defMonth < 11 ? '0' + defMonth : defMonth; 
      const createDate = newTaskDatas.created.getFullYear() + '-'  + month + '-' + newTaskDatas.created.getDate();

      const newTask = {
        name: newTaskDatas.name,
        description: newTaskDatas.description,
        created: createDate,
      }

       const res = await fetch('http://localhost:3001/tasks/', {
        method: 'POST',
        headers: {
          'Content-type': 'application/json',
        },
        body: JSON.stringify(newTask),
      })

      const data = await res.json()
      this.tasks = await this.fetchTasks();
      this.$refs.taskc.setTaskToGive(this.tasks.filter((task) => task.completed === false));
    },
    async changeCompleted(id){
      
        await fetch('http://localhost:3001/tasks/complete/' + id, {
        method: 'PATCH',
        headers: {
          'Content-type': 'application/json',
        }
      })

    this.tasks = await this.fetchTasks();
      this.$refs.taskc.setTaskToGive(this.tasks.filter((task) => task.completed === false));
      this.$refs.sideBar.reRender();
    },
    async changeProgress(id){
      console.log(id)
      await fetch('http://localhost:3001/tasks/chanegProgress/' + id, {
        method: 'PATCH',
        headers: {
          'Content-type': 'application/json',
        }
      })

    this.tasks = await this.fetchTasks();
      this.$refs.taskc.setTaskToGive(this.tasks.filter((task) => task.completed === false));
      this.$refs.sideBar.reRender();
    },
    async fetchTasks() {
      const res = await fetch('http://localhost:3001/tasks/');
      const data = await res.json();
      return data;
    },
  },
  async created(){
    this.tasks = await this.fetchTasks();
    this.$refs.taskc.setTaskToGive(this.tasks.filter((task) => task.completed === false));
    this.$refs.sideBar.reRender();
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
   
  border: 0;
  height: auto;
}

}
</style>
