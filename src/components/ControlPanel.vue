<template>
  <div class="wrapper">
    <div class="icon-button">
      <img class="svg-icon music-icon" src="../assets/icons/MusicSymbol.svg" alt="Toggle music">
      <div class="inner-shadow"></div>
      <div class="control-music"></div>
    </div>
   
    <div class="icon-button">
      <img class="svg-icon mountain-icon" src="../assets/icons/Mountains.svg" alt="Toggle landscape">
      <div class="inner-shadow"></div>
      <div class="control-landscape"></div>
    </div>
  </div>
</template>

<script>
// <button @click="$emit('toggle-music')">Toggle Music</button>
export default {
  name: "ControlPanel",
  props: {
    isMusicEnabled: Boolean,
  },
};
</script>

<style scoped>
* {
  transition: all 0.2s ease-in-out;
}

.wrapper {
  position: absolute;
  bottom: 0;
  left: 0;
  
  display: flex;
  flex-direction: column;
  gap: 10px;

  padding: 20px;
}

.svg-icon {
  z-index: 1;
  position: relative;
  background-color: transparent;
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
  
  border-radius: 50%;
}

.icon-button {
  display: flex;
  justify-content: center;
  align-items: center;

  cursor: pointer;
  width: 65px;
  height: 65px;

  border: 2px solid #FCFCF3;
  filter: drop-shadow(0 0 2px #FCFCF3);
  border-radius: 50%;
}

.icon-button:hover .inner-shadow {
  -moz-box-shadow: inset 0 0 2px #000000;
  -webkit-box-shadow: inset 0 0 2px #000000;
  box-shadow: inset 0 0 2px #000000;
}

.music-icon {
  padding-right: 6px;
}
</style>
