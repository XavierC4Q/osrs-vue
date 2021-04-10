<template>
  <div class="mt-4 shadow-md rounded mx-auto p-4 bg-yellow-50 container text-center">
    <template v-if="monster.length < 1">
      <h3>No monster found</h3>
    </template>

    <template v-else>
      <h3 class="text-center capitalize">{{ monster[0].name }}</h3>

      <div
        v-if="monster.length > 1"
        class="flex flex-wrap w-8/12 mx-auto content-center justify-evenly border-2 border-yellow-300"
      >
        <button
          v-for="(tab, i) in tabs"
          :key="i"
          :class="`cursor-pointer focus:outline-none text-xl mx-2.5 my-2 w-3/12 ${
            i === activeTab ? 'active' : ''
          }`"
          @click="activeTab = i"
          >{{ tab }}</button
        >
      </div>

      <div class="flex flex-wrap justify-evenly mt-8">
        <h6>Combat Level: {{ activeMonster.combat_level }}</h6>
        <h6>Hitpoints Level: {{ activeMonster.hitpoints }}</h6>
        <h6>Attack Level: {{ activeMonster.attack_level }}</h6>
        <h6>Defence Level: {{ activeMonster.defence_level }}</h6>
        <h6>Ranged Level: {{ activeMonster.ranged_level }}</h6>
        <h6>Magic Level: {{ activeMonster.magic_level }}</h6>
      </div>

      <p class="mt-4">{{ activeMonster.examine }}</p>
    </template>
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