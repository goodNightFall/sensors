<template>
  <div class="container" v-if="show" @click="hideModal">
    <div @click.stop class="content"><slot></slot></div>
  </div>
</template>

<script setup lang="ts">
interface Props {
  show: boolean
}

const props = defineProps<Props>()

const emit = defineEmits<{
  (e: "hide", show: false): void
}>()

function hideModal() {
  emit("hide", false)
}
</script>

<style scoped>
.container {
  display: flex;
  align-items: center;
  justify-content: center;
  position: fixed;
  left: 0px;
  top: 0px;
  height: 100vh;
  width: 100vw;
  background-color: rgba(black, 0.5);
  backdrop-filter: blur(6px) brightness(80%);
  z-index: 1;
}

.content {
  padding: 25px;
  border-radius: 12px;
  background-color: rgb(47, 47, 47);
}
</style>
