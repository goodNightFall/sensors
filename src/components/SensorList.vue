<template>
  <div v-if="sensors.length > 0">
    <h3 class="title">Список датчиков</h3>
    <SensorItem
      v-for="sensor in sensors"
      :sensor="sensor"
      :key="sensor.sensor_id"
      @deleteSensor="deleteSensor"
    />
  </div>
</template>

<script lang="ts">
import { defineComponent, PropType } from "vue"
import SensorItem from "./SensorItem.vue"
import Sensor from "@/types/Sensor"

export default defineComponent({
  name: "SensorList",
  components: { SensorItem },

  props: {
    sensors: {
      type: Array as PropType<Sensor[]>,
      required: true,
    },
  },

  methods: {
    deleteSensor(id: number) {
      this.$emit("deleteSensor", id)
    },
  },

  emits: {
    deleteSensor: (id: number) => true,
  },
})
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
