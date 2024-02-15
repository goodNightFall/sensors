<template>
  <label class="checkbox">
    {{ title }}
    <input
      :checked="modelValue"
      @change="updateInput"
      type="checkbox"
      :name="name"
    />
  </label>
</template>

<script setup lang="ts">
interface Props {
  title: string
  modelValue: boolean
  name: string
}

const props = defineProps<Props>()

const emit = defineEmits<{
  (e: "update:modelValue", event: boolean): void
}>()

function updateInput(event: Event) {
  emit("update:modelValue", (event.target as HTMLInputElement).checked)
}
</script>

<style scoped>
.checkbox {
  display: flex;
  align-items: center;
  justify-content: space-between;
  width: 300px;
  margin-top: 20px;
}

@media (max-width: 820px) {
  .checkbox {
    font-size: 15px;
  }
}

@media (max-width: 420px) {
  .checkbox {
    width: 200px;
    font-size: 12px;
  }
}
</style>
