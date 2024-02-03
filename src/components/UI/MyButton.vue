<template>
  <button class="btn">
    <slot></slot>
  </button>
</template>

<script setup lang="ts"></script>

<style scoped>
.btn {
  padding: 10px 15px;
  background: none;
  color: white;
}
</style>
