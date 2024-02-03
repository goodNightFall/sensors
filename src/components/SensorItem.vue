<template>
  <div class="container">
    <div class="sensor">
      <div class="value"><strong>Название: </strong>{{ sensor.name }}</div>
      <div class="value">
        <strong>Температура: </strong
        >{{
          sensor.hasOwnProperty("temperature") ? sensor.temperature : "None"
        }}
      </div>
      <div class="value">
        <strong>Влажность: </strong
        >{{ sensor.hasOwnProperty("humidity") ? sensor.humidity : "None" }}
      </div>
    </div>
    <MyButton class="deleteBtn" @click="deleteSensor">Удалить</MyButton>
  </div>
</template>

<script setup lang="ts">
import { onMounted, onUnmounted } from "vue"
import { MyButton } from "./UI"
import Sensor from "@/types/Sensor"

interface Props {
  sensor: Sensor
}

let interval: number

const props = defineProps<Props>()

const emit = defineEmits({
  remove: (id: number) => {
    return true
  },
})

onMounted(() => {
  interval = setInterval(() => {
    props.sensor.temperature
      ? (props.sensor.temperature += getRandomInt(3) - 1)
      : null

    props.sensor.humidity
      ? props.sensor.humidity > 1
        ? (props.sensor.humidity += getRandomInt(3) - 1)
        : (props.sensor.humidity += getRandomInt(3))
      : null
  }, Math.random() * 30000)
})

onUnmounted(() => clearInterval(interval))

function getRandomInt(max: number): number {
  const randomInt = Math.floor(Math.random() * max)
  return randomInt
}

function deleteSensor() {
  emit("remove", props.sensor.sensor_id)
}
</script>

<style scoped>
.container {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 15px;
  margin-top: 15px;
  border: 2px solid rgb(114, 114, 114);
}

.sensor {
  display: flex;
}

.value {
  padding: 5px;
  width: 300px;
}

.deleteBtn {
  border: 1px solid rgb(114, 114, 114);
  border-radius: 8px;
}

.deleteBtn:hover {
  background-color: brown;
}

@media (max-width: 1120px) {
  .value {
    width: 200px;
    font-size: 15px;
  }
}

@media (max-width: 900px) {
  .sensor {
    flex-direction: column;
  }
}

@media (max-width: 420px) {
  .value {
    width: 150px;
    font-size: 12px;
  }
}
</style>
