<script setup>
import { computed, ref } from "vue";
import draggable from "vuedraggable";
import ActorItem from "@/components/ActorItem.vue";
import _ from "lodash";
const initialBreves = [
  {
    name: "Au bout de la rue",
    actors: ["Chr.", "Dan.", "Libo"],
  },
  {
    name: "Plan de carrière",
    actors: ["Véro", "Just."],
  },
  {
    name: "La rue est à tout le monde",
    actors: ["Boule", "Libo"],
  },
  {
    name: "Comme sur des roulettes",
    actors: ["Pierre", "JP"],
  },
  {
    name: "Le juste prix",
    actors: ["Pierre", "Just."],
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
    actors: ["JP", "Jeff"],
  },
  {
    name: "À la rue",
    actors: ["Véro", "Pierre"],
  },
  {
    name: "La manif pour personne",
    actors: ["Dan.", "M-Chr.", "Chr."],
  },
  {
    name: "Du balai",
    actors: ["JP", "Libo"],
  },
  {
    name: "Le pari de pascal",
    actors: [""],
  },
  {
    name: "Un bon coup de balai",
    actors: ["M-Chr.", "Xavier"],
  },
  {
    name: "Une ombre de la rue",
    actors: [],
  },
];

const breves = ref(initialBreves);

let index = 1;
breves.value.forEach((b) => (b.id = index++));

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
`,
];

const colors = [
  "#a6cee3",
  "#1f78b4",
  "#b2df8a",
  "#33a02c",
  "#fb9a99",
  "#e31a1c",
  "#fdbf6f",
  "#ff7f00",
  "#cab2d6",
  "#6a3d9a",
  "#ffff99",
  "#b15928",
];

const actors = ref(
  Object.assign(
    {},
    ..._.union(...initialBreves.map((breve) => breve.actors)).map((actor, i) => {
      return { [actor]: { symbol: symbols[i], color: colors[i] } };
    }),
  ),
);
</script>

<template>
  <main class="col-11">
    <draggable :list="breves" :disabled="false" class="list-group" item-key="name">
      <template #item="{ element }">
        <div
          class="list-group-item d-flex flex-row align-items-center justify-content-between"
        >
          {{ element.id }} - {{ element.name }}
          <div class="d-flex flex-row ml-auto">
            <ActorItem
              :actor="actor"
              :symbol="actors[actor].symbol"
              :color="actors[actor].color"
              v-for="actor in element.actors"
            />
          </div>
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
