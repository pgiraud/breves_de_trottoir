<script setup>
defineProps(["actor", "symbol", "color"]);
</script>

<template>
  <div class="border rounded px-1 mx-1" :style="{ 'background-color': `${color}cc` }">
    {{ actor }}
  </div>
</template>
