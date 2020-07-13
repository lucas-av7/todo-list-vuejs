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
  .new-task {
    margin-top: 25px;
  }

  .new-task input {
    width: 400px;
    height: 40px;
    padding: 10px;
    outline: none;
    border: none;
    border-top-left-radius: 8px;
    border-bottom-left-radius: 8px;
  }

  .new-task button {
    height: 40px;
    width: 100px;
    outline: none;
    border: none;
    background-color: seagreen;
    color: #FFF;
    border-top-right-radius: 8px;
    border-bottom-right-radius: 8px;
    cursor: pointer;
  }

  @media (max-width: 525px) {
    .new-task input {
      width: 220px;
    }

    .new-task button{
      width: 80px;
    }
  }
</style>