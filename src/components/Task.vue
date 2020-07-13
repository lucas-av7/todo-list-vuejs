<template>
  <div class="task" :class="taskState">
    <p>{{ task.name }}</p>
  </div>
</template>

<script>
export default {
  props: {
    task: { type: Object, required: true }
  },
  computed: {
    taskState() {
      return {
        done: this.task.pending,
        pending: !this.task.pending
      }
    }
  }
}
</script>

<style>
  .task {
    width: 220px;
    height: 110px;
    border-radius: 8px;
    margin: 5px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 1.5rem;
  }

  .done {
    background-color: green;
  }

  .pending {
    background-color: red;
    text-decoration: line-through;
  }
</style>