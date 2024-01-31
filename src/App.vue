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
  if(car.value.speed < car.value.maxSpeed){
    car.value.speed += car.value.speedRate
  }
}

const slowDown = () => {
  if(car.value.speed !== 0){
    car.value.speed -= car.value.speedRate
  }
}

const fullBreak = () => {
  car.value.speed = 0
}
</script>
<template>
  <div class="text-center w-100 h-100">
    <h3>Your car is {{ car.hasStarted ? "on" : "off" }}.</h3>
    <h1>{{ car.speed }}</h1><span class="small text-info">mph</span>
    <p>Current speed</p>
    <div class="small text-danger">Max speed is {{ car.maxSpeed }}</div>
    <div>
      <button @click="gas" class="btn btn-success m-1" :disabled="(car.speed === car.maxSpeed) || (!car.hasStarted)">Gas</button>
      <button @click="slowDown" class="btn btn-warning m-1" :disabled="car.speed === 0">Slow down</button>
      <button @click="turnKey" :disabled="car.hasStarted && car.speed > 0" class="btn btn-primary m-1">{{ !car.hasStarted ? "Turn on" : "Turn off" }}</button>
      <button @click="fullBreak" class="btn btn-danger m-1" :disabled="car.speed === 0">Full Break</button>
    </div>
  </div>
</template>