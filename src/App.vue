<template>
  <div id="app">
    <div class="container">
      <PhoneConcept />
      <div class="aplicativo">
        <h1 class="titulo">Lista de tarefas</h1>
        <transition name="fade">
          <NewTask v-if="newTaskView" :tasks="tasks" :addTask="addTask" @closeAddTask="newTaskView = false" />
        </transition>  
        <ButtonAddTask @clickButton="newTaskView = true" />
        <div class="frase-inicio" v-if="tasks.length == 0">
          <img src="./assets/tasks.png" alt="New Tasks">
          <p class="frase-inicio">Adicione novas tarefas :)</p>
        </div>
        <template v-else>
          <ProgressBar :tasks="tasks" />
          <TaskGrid :tasks="tasks" @deleteTask="deleteTask" />
        </template>
      </div>
    </div>
  </div>
</template>

<script>
import NewTask from './components/NewTask'
import TaskGrid from './components/TaskGrid'
import ProgressBar from './components/ProgressBar'
import PhoneConcept from './components/PhoneConcept'
import ButtonAddTask from './components/ButtonAddTask'

export default {
  name: 'App',
  components: { NewTask, TaskGrid, ProgressBar, PhoneConcept, ButtonAddTask },
  data() {
    return {
      tasks: [],
      newTaskView: false,
    }
  },
  methods: {
    addTask(task) {
      let taskLowerCase = task.toLowerCase()
      let isUnique = this.tasks.filter(t => t.name === taskLowerCase).length === 0
      if(isUnique && taskLowerCase !== '') {
        this.tasks.push({ name: taskLowerCase, pending: true })
      }
      this.newTaskView = false
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
    },
    newTaskView() {
      const app = document.querySelector('.aplicativo')
      if (this.newTaskView) {
        app.style.overflowY = 'hidden'
      } else {
        app.style.overflowY = 'scroll'
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
    user-select: none;
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
    background-color: white;
    border-radius: 25px;
    overflow: hidden;
  }

  .aplicativo {
    width: calc(100% - 16px);
    height: calc(100% - 16px);
    padding: 10px;
    display: flex;
    flex-direction: column;
    align-items: center;
    z-index: 1;
    position: relative;
  }

  ::-webkit-scrollbar {
    width: 0px;
    background: transparent; /* make scrollbar transparent */
  }

  .titulo {
    font-size: 1.8rem;
    margin-top: 30px;
    margin-bottom: 10px;
  }

  .frase-inicio {
    font-size: 1.1rem;
    display: flex;
    flex-direction: column;
    align-items: center;
  }

  .frase-inicio img {
    width: 80%;
    margin-top: 90px;
  }

/* Transitions */
@keyframes fade-in {
  from { opacity: 0; }
  to { opacity: 1; }
}

@keyframes fade-out {
  from { opacity: 1; }
  to { opacity: 0; }
}

.fade-enter-active {
  animation: fade-in 0.2s ease;
}
.fade-leave-active {
    animation: fade-out 0.2s ease;
}

</style>
