<template>
  <div id="app">
    <div class="container">
      <h1 class="titulo">Lista de tarefas</h1>
      <NewTask :tasks="tasks" :addTask="addTask" />
      <ProgressBar v-if="tasks.length > 0" :tasks="tasks" />
      <p class="frase-inicio" v-else>Adicione novas tarefas :)</p>
      <TaskGrid :tasks="tasks" @deleteTask="deleteTask" />
    </div>
  </div>
</template>

<script>
import NewTask from './components/NewTask.vue'
import TaskGrid from './components/TaskGrid.vue'
import ProgressBar from './components/ProgressBar.vue'

export default {
  name: 'App',
  components: { NewTask, TaskGrid, ProgressBar },
  data() {
    return {
      tasks: []
    }
  },
  methods: {
    addTask(task) {
      let taskLowerCase = task.toLowerCase()
      let isUnique = this.tasks.filter(t => t.name === taskLowerCase).length === 0
      if(isUnique && taskLowerCase !== '') {
        this.tasks.push({ name: taskLowerCase, pending: true })
      }
    },
    deleteTask(i) {
      this.tasks.splice(i, 1)
    }
  },
  watch: {
    tasks: {
      deep: true,
      handler() {
        localStorage.setItem('tasks', JSON.stringify(this.tasks))
      }
    }
  },
  created() {
    this.tasks = JSON.parse(localStorage.getItem('tasks')) || []
  }
}
</script>

<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  body {
    background: #DBE6F6;  /* fallback for old browsers */
    background: -webkit-linear-gradient(to right, #C5796D, #DBE6F6);
    background: linear-gradient(to right, #C5796D, #DBE6F6);
    font-family: 'Roboto', sans-serif;
    font-size: 62.5%;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  #app {
    width: 100%;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .container {
    width: 380px;
    height: 550px;
    margin: 0 auto;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    border: 2px solid black;
    border-radius: 25px;
    background-color: white;
  }

  .titulo {
    font-size: 3.0rem;
  }

  .frase-inicio {
    margin-top: 25px;
    font-size: 1.5rem;
  }
</style>
