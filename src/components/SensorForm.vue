<template>
  <form class="container" @submit.prevent>
    <h4 class="title">Добавление датчика</h4>
    <input
      v-model="sensor.name"
      class="input"
      type="text"
      placeholder="Название"
    />

    <MyCheckbox title="Датчик измеряет температуру?" v-model="hasTemperature" />
    <MyCheckbox title="Датчик измеряет влажность?" v-model="hasHumidity" />
    <MyButton class="addBtn" @click="createSensor">Добавить</MyButton>
  </form>
</template>

<script lang="ts">
import { defineComponent } from "vue"
import { MyButton, MyCheckbox } from "./UI"

import Sensor from "../types/Sensor"

interface State {
  sensor: {
    name: string
  }

  hasTemperature: boolean
  hasHumidity: boolean
}

export default defineComponent({
  name: "SensorForm",
  components: {
    MyButton,
    MyCheckbox,
  },

  data(): State {
    return {
      sensor: {
        name: "",
      },

      hasTemperature: false,
      hasHumidity: false,
    }
  },

  methods: {
    getRandomInt(max: number, negative: boolean): number {
      const randomInt = Math.floor(Math.random() * max)
      return negative ? randomInt - max / 2 : randomInt
    },

    // Функция, очищающая форму
    clearForm() {
      this.sensor.name = ""
      this.hasTemperature = false
      this.hasHumidity = false
    },

    createSensor() {
      if (!this.sensor.name.length) {
        alert("Введите название датчика!")
        return
      }

      const newSensor: Sensor = {
        sensor_id: Date.now(),
        name: this.sensor.name,
      }

      this.hasTemperature &&
        (newSensor.temperature = this.getRandomInt(50, true))
      this.hasHumidity && (newSensor.humidity = this.getRandomInt(60, false))

      this.$emit("createSensor", newSensor)
      this.clearForm()
    },
  },

  emits: {
    createSensor: (sensor: Sensor) => true,
  },
})
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
