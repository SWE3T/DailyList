<template>
  <div class="wrapper">
   <div class="list-box">
      <img class="svg-icon mountain-icon" src="../assets/icons/Mountains.svg" alt="Toggle landscape">
      <div class="inner-shadow"></div>
      <div>Today's tasks</div>
      <hr>
      <div class="control-landscape"></div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TaskList',
  props: {
    msg: String
  }
}
</script>

<style scoped>
.wrapper {
  width: 40%;
  margin: 0 auto;
  font-size: 1.5rem;
}

.inner-shadow {
  width: 100%;
  height: 100%;

  position: absolute;
  top: 0;
  left: 0;
  
  -moz-box-shadow: inset 0 0 4px #000000;
  -webkit-box-shadow: inset 0 0 4px #000000;
  box-shadow: inset 0 0 4px #000000;
  
  border-radius: 48px;
}

.list-box {
  display: flex;
  justify-content: center;
  align-items: center;

  min-height: 40vw;

  border: 2px solid #FCFCF3;
  filter: drop-shadow(0 0 2px #FCFCF3);
  border-radius: 50%;
}
</style>
