<template>
  <div class="buttonAddTask">
    <button @click="$emit('clickButton')">+</button>
  </div>
</template>

<script>
export default {

}
</script>

<style>
  .buttonAddTask {
    position: absolute;
    bottom: 25px;
    z-index: 1;
  }

  .buttonAddTask button {
    width: 45px;
    height: 45px;
    border-radius: 50%;
    border: none;
    outline: none;
    box-shadow: 0px 1px 5px #000B;
    cursor: pointer;
    background-color: white;
    font-size: 2.5rem;
    color: #00BFA6;
  }

  @media screen and (max-width: 900px) {
    .buttonAddTask {
      bottom: 50px;
    }
  }
</style>