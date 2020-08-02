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
    width: 260px;
    min-height: 35px;
    padding: 5px;
    border-radius: 5px;
    margin: 5px;
    cursor: pointer;
    position: relative;
    user-select: none;
    line-height: 1.5rem;
  }

  .task p {
    text-align: left;
    width: 100%;
    word-wrap: break-word;
    font-size: 1.0rem;
    padding-right: 20px;
  }

  .done {
    background-color: #25af25;
    text-decoration: line-through;
    border-left: 10px solid #086d08;
  }

  .pending {
    background-color: tomato;
    border-left: 10px solid #b32e2e;
  }

  .close {
    width: 18px;
    height: 18px;
    border-radius: 50%;
    position: absolute;
    right: 6px;
    top: 6px;
    font-size: 0.8rem;
    line-height: 0.8rem;
    display: flex;
    align-items: center;
    justify-content: center;

  }

  .done .close {
    background-color: #086d08;
    color: #25af25;
  }

  .pending .close {
    background-color: #b32e2e;
    color: tomato;
  }
</style>