<template>
  <div class="tasks">
    <Task v-for="(task, i) in tasks" :key="task.name" :task="task"
      @deleteTask="$emit('deleteTask', i)" />
  </div>
</template>

<script>
import Task from './Task.vue'

export default {
  components: { Task },
  props: {
    tasks: { type: Array, required: true }
  }
}
</script>

<style>
  .tasks {
    width: 100%;
    display: flex;
    justify-content: center;
    flex-wrap: wrap;
  }
</style>