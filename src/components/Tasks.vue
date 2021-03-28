<template>
  <div :key="task.id"  v-for="task in tasks">
    <Task @changeCompleted="$emit('changeCompleted', task.id)" @changeProgress="$emit('changeProgress', task.id)"  :task="task" />
  </div>
</template>

<script>
import Task from './Task';

export default {
  name: 'Tasks',
    components: {
        Task
    },
    props:{
      tasks: Array
    },
  emits:['changeCompleted', 'changeProgress']
}
</script>

<style scoped>

div:last-child{
  margin-bottom: 1em;
}

</style>
