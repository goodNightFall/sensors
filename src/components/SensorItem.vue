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

<script lang="ts">
import { defineComponent, PropType } from "vue"
import { MyButton } from "./UI"
import Sensor from "@/types/Sensor"

interface State {
  interval: number
  isVisible: boolean
}

export default defineComponent({
  name: "SensorItem",

  data(): State {
    return {
      interval: 0,
      isVisible: false,
    }
  },

  components: {
    MyButton,
  },

  props: {
    sensor: {
      type: Object as PropType<Sensor>,
      required: true,
    },
  },

  mounted() {
    // Запускается setInterval, который меняет значения температуры и влажности датчиков
    this.interval = setInterval(() => {
      this.sensor.temperature
        ? (this.sensor.temperature += this.getRandomInt(3) - 1)
        : null

      this.sensor.humidity
        ? this.sensor.humidity > 1
          ? (this.sensor.humidity += this.getRandomInt(3) - 1)
          : (this.sensor.humidity += this.getRandomInt(3))
        : null
    }, Math.random() * 30000)
  },

  unmounted() {
    clearInterval(this.interval)
  },

  methods: {
    deleteSensor() {
      this.$emit("deleteSensor", this.sensor.sensor_id)
    },

    getRandomInt(max: number): number {
      const randomInt = Math.floor(Math.random() * max)
      return randomInt
    },
  },

  emits: {
    deleteSensor: (id: number) => true,
  },
})
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
