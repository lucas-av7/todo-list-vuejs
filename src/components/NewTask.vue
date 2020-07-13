<template>
  <div class="new-task">
    <input type="text" v-model="taskText" @keypress.enter="addTask(taskText), taskText = ''" >
    <button @click="addTask(taskText), taskText = ''">Adicionar</button>
  </div>
</template>

<script>
export default {
  props: {
    addTask: { type: Function, required: true }
  },
  data() {
    return {
      taskText: ''
    }
  }
}
</script>

<style>

</style>