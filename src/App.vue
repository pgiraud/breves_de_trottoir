<script setup>
import { computed, ref } from "vue";
import draggable from "vuedraggable";
import _ from "lodash";
const breves = ref([
  {
    name: "Au bout de la rue",
    actors: ["Christine", "Danièle", "Libo"],
  },
  {
    name: "Plan de carrière",
    actors: ["Véronique", "Justine"],
  },
  {
    name: "La rue est à tout le monde",
    actors: ["Brigitte", "Libo"],
  },
  {
    name: "Comme sur des roulettes",
    actors: ["Pierre", "Jean-Pierre"],
  },
  {
    name: "Le juste prix",
    actors: ["Pierre", "Justine"],
  },
  {
    name: "L'homme de la rue",
    actors: ["Pierre", "Xavier"],
  },
  {
    name: "Le bon numéro",
    actors: ["Sophie", "Xavier"],
  },
  {
    name: "Deuxième chance",
    actors: ["Jean-Pierre", "Jeff"],
  },
  {
    name: "À la rue",
    actors: ["Véronique", "Pierre"],
  },
  {
    name: "La manif pour personne",
    actors: ["Danièle", "Marie-Christine", "Christine"],
  },
  {
    name: "Du balai",
    actors: ["Jean-Pierre", "Libo"],
  },
  {
    name: "Le pari de pascal",
    actors: [""],
  },
  {
    name: "Un bon coup de balai",
    actors: ["Marie-Christine", "Xavier"],
  },
  {
    name: "Une ombre de la rue",
    actors: [],
  },
])

let index = 1;
breves.value.forEach((b) => b.id = index++);

const actors = computed(() => _.union(...breves.value.map((breve) => breve.actors)));

const symbols = [
`
<!-- Class 1: Empty Circle -->
<svg viewBox="0 0 24 24">
  <circle cx="12" cy="12" r="10" stroke="black" stroke-width="2" fill="none"/>
</svg>

`,
`
<!-- Class 2: Filled Circle -->
<svg viewBox="0 0 24 24">
  <circle cx="12" cy="12" r="10" fill="black"/>
</svg>

`,
`
<!-- Class 3: Hatched Circle -->
<svg width="100" height="100" viewBox="0 0 24 24">
  <circle cx="12" cy="12" r="10" stroke="black" stroke-width="2" fill="none"/>
  <defs>
    <pattern id="hatched" patternUnits="userSpaceOnUse" width="4" height="4">
      <path d="M0,0 L4,4 M4,0 L0,4" stroke="black" stroke-width="1"/>
    </pattern>
  </defs>
  <circle cx="12" cy="12" r="9" fill="url(#hatched)"/>
</svg>

`,
`
<!-- Class 4: Empty Triangle -->
<svg width="100" height="100" viewBox="0 0 24 24">
  <polygon points="12,2 2,22 22,22" stroke="black" stroke-width="2" fill="none"/>
</svg>

`,
`
<!-- Class 5: Filled Triangle -->
<svg width="100" height="100" viewBox="0 0 24 24">
  <polygon points="12,2 2,22 22,22" fill="black"/>
</svg>
`,
`
<!-- Class 6: Hatched Triangle -->
<svg viewBox="0 0 24 24">
  <polygon points="12,2 2,22 22,22" stroke="black" stroke-width="2" fill="none"/>
  <polygon points="12,3 3,21 21,21" fill="url(#hatched)"/>
</svg>

`,
`
<!-- Class 7: Empty Square -->
<svg viewBox="0 0 24 24">
  <rect x="4" y="4" width="16" height="16" stroke="black" stroke-width="2" fill="none"/>
</svg>

`,
`
<!-- Class 8: Filled Square -->
<svg viewBox="0 0 24 24">
  <rect x="4" y="4" width="16" height="16" fill="black"/>
</svg>

`,
`
<!-- Class 9: Hatched Square -->
<svg viewBox="0 0 24 24">
  <rect x="4" y="4" width="16" height="16" stroke="black" stroke-width="2" fill="none"/>
  <rect x="5" y="5" width="14" height="14" fill="url(#hatched)"/>
</svg>
`,
`
<!-- Class 10: Empty Diamond -->
<svg width="100" height="100" viewBox="0 0 24 24">
  <polygon points="12,2 22,12 12,22 2,12" stroke="black" stroke-width="2" fill="none"/>
</svg>
`,
`
<!-- Class 11: Filled Diamond -->
<svg width="100" height="100" viewBox="0 0 24 24">
  <polygon points="12,2 22,12 12,22 2,12" fill="black"/>
</svg>
`,
`
<!-- Class 12: Hatched Diamond -->
<svg width="100" height="100" viewBox="0 0 24 24">
  <defs>
    <pattern id="hatched" patternUnits="userSpaceOnUse" width="4" height="4">
      <path d="M0,0 L4,4 M4,0 L0,4" stroke="black" stroke-width="1"/>
    </pattern>
  </defs>
  <polygon points="12,2 22,12 12,22 2,12" stroke="black" stroke-width="2" fill="url(#hatched)"/>
</svg>
`
];

</script>

<template>
  <main>
    <span v-for="actor, index in actors">
      {{ actor }}
      <span v-html="symbols[index]" class="symbol">
      </span>
    </span>
    <draggable :list="breves" :disabled="false" class="list-group" item-key="name">
      <template #item="{ element }">
        <div class="list-group-item">
          {{ element.id }} - {{ element.name }}
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
