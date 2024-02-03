<template>
  <div v-if="sensors.length > 0">
    <h3 class="title">Список датчиков</h3>
    <SensorItem
      v-for="sensor in sensors"
      :sensor="sensor"
      :key="sensor.sensor_id"
      @remove="deleteSensor"
    />
  </div>

  <div v-if="sensors.length === 0">
    <h3 class="title">Список датчиков пуст</h3>
  </div>
</template>

<script setup lang="ts">
import {} from "vue"
import SensorItem from "./SensorItem.vue"
import Sensor from "@/types/Sensor"

interface Props {
  sensors: Sensor[]
}

const props = defineProps<Props>()

const emit = defineEmits({
  remove: (id: number) => {
    return true
  },
})

function deleteSensor(id: number) {
  emit("remove", id)
}
</script>

<style scoped>
.title {
  margin: 15px 0;
  font-size: 30px;
}

@media (max-width: 820px) {
  .title {
    font-size: 20px;
  }
}
</style>
