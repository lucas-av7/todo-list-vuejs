<template>
  <div class="layout-telefone">
    <span class="docker">
      <span class="alto-falante"></span>
      <span class="camera"></span>
    </span>
  </div>
</template>

<script>
export default {

}
</script>

<style>
/* Desenho do telefone */
  .layout-telefone {
    width: 100%;
    height: 100%;
    border: 8px solid black;
    border-radius: 25px;
    position: absolute;
    top: 0;
    left: 0;
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
    z-index: 10;
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
    right: 30px;
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

  @media screen and (max-width: 900px) {
    .layout-telefone {
      display: none;
    }
  }
</style>