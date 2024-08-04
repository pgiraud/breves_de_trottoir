<script setup>
defineProps(["actor", "symbol", "color"]);
</script>

<template>
  <div
    class="d-flex flex-column align-items-center border rounded px-2"
    :style="{ 'background-color': `${color}cc` }"
    style="width: 60px"
  >
    {{ actor }}
    <span v-html="symbol" class="symbol"> </span>
  </div>
</template>
