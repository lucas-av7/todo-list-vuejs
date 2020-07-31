<template>
  <div id="app">
    <div class="container">
      <div class="layout-telefone">
        <span class="docker"></span>
        <span class="alto-falante"></span>
        <span class="camera"></span>
      </div>
      <div class="aplicativo">
        <h1 class="titulo">Lista de tarefas</h1>
        <NewTask :tasks="tasks" :addTask="addTask" />
        <ProgressBar v-if="tasks.length > 0" :tasks="tasks" />
        <p class="frase-inicio" v-else>Adicione novas tarefas :)</p>
        <TaskGrid :tasks="tasks" @deleteTask="deleteTask" />
      </div>
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
    width: 330px;
    height: 550px;
    margin: 0 auto;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    position: relative;
  }

  .aplicativo {
    width: 100%;
    height: 100%;
    padding: 20px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    z-index: 2;
  }

  .titulo {
    font-size: 2.0rem;
  }

  .frase-inicio {
    margin-top: 25px;
    font-size: 1.2rem;
  }

  /* Desenho do telefone */
  .layout-telefone {
    width: 100%;
    height: 100%;
    border: 8px solid black;
    border-radius: 25px;
    position: absolute;
    top: 0;
    left: 0;
    z-index: 1;
    background-color: white;
  }

  .docker {
    width: 180px;
    height: 33px;
    background-color: black;
    position: absolute;
    top: 0;
    left: 50%;
    transform: translateX(-50%);
    border-bottom-left-radius: 25px;
    border-bottom-right-radius: 25px;
  }

  .alto-falante {
    width: 45px;
    height: 8px;
    background: #444;
    border-radius: 10px;
    position: absolute;
    top: 10px;
    left: 50%;
    transform: translateX(-50%);
  }

  .camera {
    width: 20px;
    height: 20px;
    border-radius: 50%;
    background-color: #444;
    position: absolute;
    top: 3px;
    right: 100px;
  }

  .camera::after {
    content: '';
    width: 8px;
    height: 8px;
    border-radius: 50%;
    background-color: black;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
  }
</style>
