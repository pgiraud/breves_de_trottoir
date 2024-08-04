<script setup>
defineProps(["actor", "symbol"]);
</script>

<template>
  <div class="d-flex flex-column align-items-center border rounded px-2">
    {{ actor }}
    <span v-html="symbol" class="symbol"> </span>
  </div>
</template>
