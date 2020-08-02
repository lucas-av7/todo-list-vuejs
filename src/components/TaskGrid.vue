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
    height: 380px;
    overflow-y: scroll;
    display: flex;
    flex-direction: column;
    justify-content: flex-start;
    align-items: center;
  }

  @media screen and (max-width: 900px) {
    .tasks {
      height: calc(100vh - 200px);
    }
  }
</style>