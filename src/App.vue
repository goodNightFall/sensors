<template>
  <div class="app">
    <header class="header"><h4 class="title">Датчики</h4></header>
    <SensorForm @createSensor="createSensor" />
    <SensorList @deleteSensor="deleteSensor" :sensors="sensors" />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue"
import SensorList from "./components/SensorList.vue"
import SensorForm from "./components/SensorForm.vue"
import Sensor from "./types/Sensor"

interface State {
  sensors: Sensor[]
}

export default defineComponent({
  name: "App",
  components: { SensorList, SensorForm },

  data(): State {
    return {
      // Список датчиков, который увидит пользователь по умолчанию
      sensors: [
        {
          sensor_id: 1,
          name: "N/A",
          temperature: 20,
          humidity: 25,
        },
        {
          sensor_id: 2,
          name: "N/A",
        },
        {
          sensor_id: 3,
          name: "N/A",
          temperature: 13,
        },
        {
          sensor_id: 4,
          name: "N/A",
          humidity: 58,
        },
        {
          sensor_id: 5,
          name: "N/A",
          temperature: 23,
          humidity: 59,
        },
        {
          sensor_id: 6,
          name: "N/A",
        },
        {
          sensor_id: 7,
          name: "N/A",
          temperature: 19,
        },
        {
          sensor_id: 8,
          name: "N/A",
          humidity: 35,
        },
        {
          sensor_id: 9,
          name: "N/A",
          temperature: 22,
          humidity: 50,
        },
        {
          sensor_id: 10,
          name: "N/A",
        },
        {
          sensor_id: 11,
          name: "N/A",
          temperature: 20,
        },
        {
          sensor_id: 12,
          name: "N/A",
          humidity: 57,
        },
        {
          sensor_id: 13,
          name: "N/A",
          temperature: 22,
          humidity: 55,
        },
        {
          sensor_id: 14,
          name: "N/A",
        },
        {
          sensor_id: 15,
          name: "N/A",
          temperature: 13,
        },
        {
          sensor_id: 16,
          name: "N/A",
          humidity: 45,
        },
        {
          sensor_id: 17,
          name: "N/A",
          temperature: 21,
          humidity: 35,
        },
        {
          sensor_id: 18,
          name: "N/A",
        },
        {
          sensor_id: 19,
          name: "N/A",
          temperature: 20,
        },
        {
          sensor_id: 20,
          name: "N/A",
          humidity: 35,
        },
      ],
    }
  },

  mounted() {
    // Проверяем лежит ли массив датчиков в Local Storage
    if (localStorage.getItem("sensors")) {
      const tempData = localStorage.getItem("sensors")
      tempData ? (this.sensors = JSON.parse(tempData)) : null
    }

    window.addEventListener("beforeunload", this.saveSensors)
  },

  unmounted() {
    window.removeEventListener("beforeunload", this.saveSensors)
  },

  methods: {
    createSensor(sensor: Sensor) {
      // Функция, которая добавляет датчик в массив
      this.sensors.unshift(sensor)
    },

    deleteSensor(id: number) {
      // Функция, которая удаляет датчик из массива
      this.sensors = this.sensors.filter((sensor) => id !== sensor.sensor_id)
    },

    saveSensors() {
      // Функция, которая сохраняет наш массив в Local Storage
      const parsed = JSON.stringify(this.sensors)
      localStorage.setItem("sensors", parsed)
    },
  },
})
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: "Poppins", sans-serif;
  background-color: #141414;
  color: white;
}

::-webkit-scrollbar {
  width: 0;
}

.app {
  padding: 50px 200px;
}

.header {
  display: flex;
  margin-bottom: 25px;
}

.title {
  font-size: 50px;
}

@media (max-width: 1420px) {
  .app {
    padding: 50px;
  }
}

@media (max-width: 820px) {
  .title {
    font-size: 30px;
  }
}

@media (max-width: 420px) {
  .app {
    padding: 20px;
  }
}
</style>
