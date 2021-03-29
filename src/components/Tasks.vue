<template>
  <div :key="task._id"  v-for="task in tasks">
    <Task @changeCompleted="$emit('changeCompleted', task._id)" @changeProgress="$emit('changeProgress', task._id)"  :task="task" />
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
