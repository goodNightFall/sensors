<template>
  <label class="checkbox">
    {{ title }}
    <input :checked="modelValue" @change="updateInput" type="checkbox" />
  </label>
</template>

<script lang="ts">
import { defineComponent } from "vue"

export default defineComponent({
  name: "MyCheckbox",

  props: {
    title: String,
    modelValue: Boolean,
  },

  methods: {
    updateInput(event: Event) {
      this.$emit(
        "update:modelValue",
        (event.target as HTMLInputElement).checked
      )
    },
  },
})
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
