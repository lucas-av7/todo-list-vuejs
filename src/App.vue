<template>
  <div id="app">
    <h1 class="titulo">Lista de tarefas</h1>
    <NewTask />
    <TaskGrid :tasks="tasks" />
  </div>
</template>

<script>
import NewTask from './components/NewTask.vue'
import TaskGrid from './components/TaskGrid.vue'

export default {
  name: 'App',
  components: { NewTask, TaskGrid },
  data() {
    return {
      tasks: [
        { name: 'Jogar o lixo', pending: true },
        { name: 'Jogar bola', pending: false },
      ]
    }
  }
}
</script>

<style>
  * {
    margin: 0;
    padding: 0;
  }

  body {
    background: #DBE6F6;  /* fallback for old browsers */
    background: -webkit-linear-gradient(to right, #C5796D, #DBE6F6);
    background: linear-gradient(to right, #C5796D, #DBE6F6);
    font-family: 'Roboto', sans-serif;
    font-size: 62.5%;
  }

  #app {
    max-width: 960px;
    min-height: 100vh;
    margin: 0 auto;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  .titulo {
    font-size: 3.0rem;
  }
</style>
