<template>
  <div class="mt-4 shadow-md rounded w-auto p-4">
    <h3>{{ monster[0].name }}</h3>

    <div
      v-if="monster.length > 1"
      class="flex flex-wrap w-full"
    >
      <span
        v-for="(t, i) in tabs"
        :key="i"
        :class="`w-2/12 ${i === activeTab ? 'active' : ''}`"
        >{{ t }}</span
      >
    </div>

    <div class="flex flex-wrap">
      <h6 class="sm:w-2/12">
        Combat Level {{ activeMonster.combat_level }}
      </h6>
      <h6 class="sm:w-2/12">
        Hitpoints Level {{ activeMonster.hitpoints }}
      </h6>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from 'vue'

interface IMonster {
  _id: string
  attack_level: number
  combat_level: number
  defence_level: number
  examine: string
  hitpoints: number
  magic_level: number
  name: string
  ranged_level: number
}

export default Vue.extend({
  name: 'Monster-Basic-Vue',
  data: () => ({
    activeTab: 0,
  }),
  computed: {
    activeMonster() {
      const selectedMonster = this.monster[this.activeTab]

      return selectedMonster
    },
    tabs() {
      return this.monster.map((m) => `Level ${m.combat_level}`)
    },
  },
  props: {
    monster: { type: Array as () => IMonster[], required: true },
  },
})
</script>