<script setup>
import { ref } from "vue"

const car = ref({
  hasStarted: false,
  speed: 0,
  speedRate: 20,
  maxSpeed: 200,
})

const message = ref("")

const turnKey = () => {
  car.value.hasStarted = !car.value.hasStarted
}

const gas = () => {
  if (car.value.speed < car.value.maxSpeed) {
    car.value.speed += car.value.speedRate
  }
}

const slowDown = () => {
  if (car.value.speed !== 0) {
    car.value.speed -= car.value.speedRate
  }
}

const fullBreak = () => {
  car.value.speed = 0
}
</script>
<template>
  <main>
  <div class="text-center">
    <iframe src="https://giphy.com/embed/4LyAxhbSz1NsZMO91G" v-if="car.hasStarted && car.speed === 0" width="480"
      height="396" frameBorder="0" class="giphy-embed" allowFullScreen></iframe>
    <iframe src="https://giphy.com/embed/7hAr7m8m7k3uumlu4G" v-if="car.speed > 0" width="480" height="194" frameBorder="0"
      class="giphy-embed" allowFullScreen></iframe>
    <h3>Your car is {{ car.hasStarted ? "on" : "off" }}.</h3>
    <h1>{{ car.speed }}</h1><span class="small text-info">mph</span>
    <p>Current speed</p>
    <div class="small text-danger">Max speed is {{ car.maxSpeed }}</div>
    <div>
      <button @click="gas" class="btn btn-success m-1"
        :disabled="(car.speed === car.maxSpeed) || (!car.hasStarted)">Gas</button>
      <button @click="slowDown" class="btn btn-warning m-1" :disabled="car.speed === 0">Slow down</button>
      <button @click="turnKey" :disabled="car.hasStarted && car.speed > 0" class="btn btn-primary m-1">{{
        !car.hasStarted ? "Turn on" : "Turn off" }}</button>
      <button @click="fullBreak" class="btn btn-danger m-1" :disabled="car.speed === 0">Full Break</button>
    </div>
  </div>
</main>
</template>
<style scoped>
  main{
    height: 100vh;
    width: 100vw;
    background-color:dimgrey ;
    display:flex;
    justify-content: center;
    align-items: center;
  }
</style>