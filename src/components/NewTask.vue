<template>
  <div class="new-task">
    <div class="overlay" @click="$emit('closeAddTask')"></div>
    <div class="input-field">
      <input ref="inputFocus" type="text" v-model.trim="taskText"
        placeholder="Nova tarefa" 
        @keypress.enter="addTask(taskText), taskText = ''" >
      <button @click="addTask(taskText), taskText = ''">Salvar</button>
    </div>
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
  },
  mounted() {
    this.$refs.inputFocus.focus()
  }
}
</script>

<style>
  .new-task {
    z-index: 2;
    width: 100%;
    height: 100%;
    position: absolute;
    top: 0;
    left: 0;
  }

  .overlay {
    width: 100%;
    height: 100%;
    background-color: #000A;
    cursor: pointer;
  }

  .input-field {
    position: absolute;
    bottom: 0;
    left: 0;
    width: 314px;
    height: 120px;
    background-color: white;
    border-bottom-left-radius: 20px;
    border-bottom-right-radius: 20px;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .new-task input {
    width: 200px;
    height: 40px;
    padding: 10px;
    outline: none;
    border: none;
    font-size: 1.0rem;
  }

  .new-task button {
    height: 40px;
    width: 70px;
    outline: none;
    border: none;
    color: #00BFA6;
    background-color: transparent;
    cursor: pointer;
    font-size: 1.0rem;
  }
</style>