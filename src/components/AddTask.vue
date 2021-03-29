<template>
    <form  @submit="onSubmit" class="conatiner"> 
      <div class="header">
        <div class="task-name">
            <label> Task name:</label> 
            <input type="text" v-model="taskName" name="name" placeholder="Make the user schema" maxlength="50" > 
        </div>
        <div class="btn">
           <input type="submit" value="Add" class="sb-btn" />
        </div>
      </div>
      <div class="t-area">
        <label >{{label_name}}</label> 
        <textarea rows="8" maxlength="435" v-model="description" name="description" placeholder="Lorem ipsum dolor sit amet, consectetur adipiscing elit. Morbi iaculis pellentesque arcu, sit amet elementum ipsum sodales laoreet. Fusce feugiat eget velit ac sollicitudin. Fusce nec augue nulla. Nulla ullamcorper! Lorem ipsum dolor sit amet, consectetur adipiscing elit. Morbi iaculis pellentesque arcu, sit amet elementum ipsum sodales laoreet. Fusce feugiat eget velit ac sollicitudin. Fusce nec augue nulla. Nulla ullamcorper!Lorem ipsum dolor sit amet, consectetur adipiscing elit. Morbi iaculis pellentesque arcu, sit amet elementum ipsum sodales laoreet. Fusce feugiat eget velit ac sollicitudin. Fusce nec augue nulla. Nulla ullamcorper!">  </textarea>
      </div>
    </form >
</template>

<script>
export default {
  name: 'AddTask',
  data(){
    return{
      taskName: '',
      description: ''
    }
  },
  methods:{
    onSubmit(e){
      e.preventDefault();
      
        if(!this.taskName){
          alert('Task must have a name!');
          return;
        }

        if(!this.description){
          alert('Task must have a description!');
          return;
        }

        if(this.taskName.length < 4){
          alert('Task name  must need to be at least 3 character!');
          return;
        } 

        if(this.description.length < 4){
          alert('Task description must need to be at least 3 character!');
          return;
        }
      

      const newTaskDatas = {
        name: this.taskName,
        description: this.description,
        created: new Date()
      };

      this.$emit('add-task', newTaskDatas);

      this.taskName = '';
      this.description = '';


    }
  }
    
  }

</script>

<style scoped>
.conatiner {
  padding: 15px;
  width: 50%;
  display: grid;
  grid-template-columns: 1fr;
}
.clearfix {
  clear: both;
}
.header{
  display: grid;
  grid-template-columns: 2fr 1fr;
}


.task-name >input {
  width: 100%;
}
.t-area{
  margin-top: 0.7em;
  max-width: 100%;
}

textarea{ resize: none;
    background: #D8D8D8;
    border: 0;
    border-radius:15px;
    box-sizing: border-box;
    text-align: justify;
    width: 100%;
    padding: 1em
}


input{
    box-sizing: border-box;
    background: #D8D8D8;
    border: 0;
    border-radius:15px;
    padding: 0.9em;
}


.btn{
  margin-right: 0;
  justify-self: end;
  align-self: center;
}

.input{ 
  justify-self: start;
}

.tarea{
  width:90%;
  margin: 0 auto;
}

.sb-btn{
    border-radius: 15px;
    border: 0;
    width: 7em;
    background: #797979;
    color: white;
}


@media screen and (max-width: 992px) {
  
  .header{
    display: grid;
    grid-template-columns: 1fr;
  }

  .btn{
    grid-row: 1;
  }
}
</style>