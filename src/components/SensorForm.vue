<template>
  <form class="container" @submit.prevent>
    <h4 class="title">Добавление датчика</h4>
    <input
      v-model="name"
      class="input"
      type="text"
      placeholder="Название"
      name="sensor-name"
    />

    <BaseCheckbox
      title="Датчик измеряет температуру?"
      v-model="hasTemperature"
      name="sensor-temperature"
    />
    <BaseCheckbox
      title="Датчик измеряет влажность?"
      v-model="hasHumidity"
      name="sensor-humidity"
    />
    <BaseButton class="addBtn" @click="createSensor">Добавить</BaseButton>
  </form>
</template>

<script setup lang="ts">
import { ref } from "vue"
import { BaseButton, BaseCheckbox } from "./UI"
import Sensor from "../types/Sensor"

const name = ref("")
const hasTemperature = defineModel<boolean>("hasTemperature")
const hasHumidity = defineModel<boolean>("hasHumidity")

const emit = defineEmits({
  create: (sensor: Sensor) => {
    return true
  },
})

function createSensor() {
  if (!name.value.length) {
    alert("Введите название датчика!")
    return
  }

  const newSensor: Sensor = {
    sensor_id: Date.now(),
    name: name.value,
  }

  hasTemperature.value && (newSensor.temperature = getRandomInt(50, true))
  hasHumidity.value && (newSensor.humidity = getRandomInt(60, false))

  emit("create", newSensor)
  clearForm()
}

function getRandomInt(max: number, negative: boolean): number {
  const randomInt = Math.floor(Math.random() * max)
  return negative ? randomInt - max / 2 : randomInt
}

function clearForm() {
  name.value = ""
  hasTemperature.value = false
  hasHumidity.value = false
}
</script>

<style scoped>
.addBtn {
  margin-top: 15px;
  align-self: self-end;
  background-color: rgb(29, 60, 236);
  border: none;
  border-radius: 8px;
}
.container {
  display: flex;
  flex-direction: column;
}

.title {
  font-size: 30px;
}
.input {
  width: 100%;
  padding: 10px 15px;
  margin-top: 15px;
  border: 2px solid rgb(114, 114, 114);
}

@media (max-width: 820px) {
  .title {
    font-size: 20px;
  }
}
</style>
