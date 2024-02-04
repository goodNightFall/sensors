<template>
  <BaseModal @hide="hideModal"
    ><div class="container">
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
      <BaseButton class="deleteBtn" @click="removeSensor">Удалить</BaseButton>
    </div>
  </BaseModal>
</template>

<script setup lang="ts">
import { BaseButton, BaseModal } from "./UI"
import Sensor from "@/types/Sensor"

interface Props {
  sensor: Sensor
}

const props = defineProps<Props>()

const emit = defineEmits<{
  (e: "hide", show: boolean): void
  (e: "remove"): void
}>()

function hideModal(show: boolean) {
  emit("hide", show)
}

function removeSensor() {
  emit("remove")
}
</script>

<style scoped>
.container {
  display: flex;
  padding: 15px;
  margin-top: 15px;
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
