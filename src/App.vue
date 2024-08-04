<script setup>
import { computed, ref } from "vue";
import draggable from "vuedraggable";
const breves = ref([
  {
    name: "L'homme de la rue",
    actors: ["Pierre", "Xavier"],
  },
  {
    name: "Comme sur des roulettes",
    actors: ["Pierre", "Jean-Pierre"],
  },
  {
    name: "Le juste prix",
    actors: ["Pierre", "Justine"],
  }
])
</script>

<template>
  <main>
    <draggable :list="breves" :disabled="false" class="list-group" item-key="name">
      <template #item="{ element }">
        <div class="list-group-item">
          {{ element.name }}
        </div>
      </template>
    </draggable>
  </main>
</template>

<style scoped>
header {
  line-height: 1.5;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}
</style>
