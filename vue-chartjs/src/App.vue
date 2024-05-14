<template>
  <div class="weekly">
    <Weekly />
  </div>
  <div class="yearly">
    <Monthly />
  </div>
  <div class="yearly">
    <Yearly />
  </div>
</template>

<script setup>
import Weekly from './components/Weekly.vue';
import Monthly from './components/Montly.vue';
import Yearly from './components/Yearly.vue';
</script>

<style>
body {
  margin: 0;
}

#app {
  display: flex;
  flex-direction: column;
  font-family:Helvetica;
  margin: 10px;
  width: 70%;
}

.weekly {
  display: flex;
  border: rgba(190, 190, 190, 0.527) solid 1px;
  border-radius: 5px;
  margin: 10px;
}

.yearly {
  display: flex;
  border: rgba(190, 190, 190, 0.527) solid 1px;
  border-radius: 5px;
  margin: 10px;
}

</style>
