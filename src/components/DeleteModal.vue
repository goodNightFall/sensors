<template>
  <BaseModal>
    <div class="container">
      <h3 class="title">Подтвердите удаление!</h3>
      <div class="value"><strong>Название: </strong>{{ sensor.name }}</div>
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
  (e: "remove"): void
}>()

function removeSensor() {
  emit("remove")
}
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  padding: 15px;
}

.title {
  font-size: 30px;
}

.value {
  font-size: 20px;
  margin-block: 25px;
}

.deleteBtn {
  border: 1px solid rgb(114, 114, 114);
  border-radius: 8px;
}

.deleteBtn:hover {
  background-color: brown;
}
</style>
