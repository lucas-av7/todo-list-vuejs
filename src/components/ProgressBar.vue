<template>
  <div class="progress-bar">
    <p class="progress">{{ progress }}%</p>
    <div class="bar" :style="{ width: progress + '%' }"></div>
  </div>
</template>

<script>
export default {
  props: {
    tasks: { type: Array, required: true }
  },
  computed: {
    progress() {
      let total = this.tasks.length
      let done = this.tasks.filter(t => t.pending === false).length
      return Math.round((done / total) * 100)
    }
  }
}
</script>

<style>
  .progress-bar {
    width: 80%;
    height: 30px;
    border: 2px solid #000;
    border-radius: 8px;
    margin: 15px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    position: relative;
  }

  .progress {
    z-index: 1;
    font-size: 1.0rem;
  }

  .bar {
    height: 100%;
    position: absolute;
    background-color: green;
    border-radius: 8px;
    align-self: flex-start;
  }
</style>