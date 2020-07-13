<template>
  <div class="task" :class="taskState"
    @click="toggleState">
    <span class="close" @click.stop="$emit('deleteTask')">x</span>
    <p>{{ task.name }}</p>
  </div>
</template>

<script>
export default {
  props: {
    task: { type: Object, required: true },
  },
  computed: {
    taskState() {
      return {
        done: !this.task.pending,
        pending: this.task.pending
      }
    }
  },
  methods: {
    toggleState() {
      this.task.pending = !this.task.pending
    }
  }
}
</script>

<style>
  .task {
    width: 220px;
    height: 110px;
    padding: 5px;
    border-radius: 8px;
    margin: 5px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 1.4rem;
    text-align: center;
    cursor: pointer;
    position: relative;
    user-select: none;
  }

  .task p {
    width: 100%;
    word-wrap: break-word;
  }

  .done {
    background-color: #007F00;
    text-decoration: line-through;
    border-left: 10px solid #004C00;
  }

  .pending {
    background-color: red;
    border-left: 10px solid #B20000;
  }

  .close {
    width: 24px;
    height: 24px;
    border-radius: 50%;
    position: absolute;
    right: 7px;
    top: 7px;
    font-size: 1rem;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .done .close {
    background-color: #004C00;
  }

  .pending .close {
    background-color: #B20000;
  }
</style>