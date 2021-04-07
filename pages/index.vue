<template>
  <div>
    <form @submit.prevent="handleSubmit">
      <input class="border-2" type="text" @input="handleInput" :value="input" />
      <button type="submit">Search</button>
    </form>

    <monster-basic-vue v-if="monster" :monster="monster" />
  </div>
</template>

<script lang="ts">
import Vue from 'vue'
import MonsterBasicVue from '~/components/monster-basic.vue'

export default Vue.extend({
  data: () => ({
    input: '',
    loading: false,
    error: false,
    monster: null,
  }),
  computed: {
    formattedMonsterName() {
      const input = this.input.toLowerCase();
      return input.charAt(0).toUpperCase() + input.slice(1)
    },
  },
  components: {
    MonsterBasicVue,
  },
  methods: {
    handleInput(e: any) {
      this.input = e.target.value
    },
    async handleSubmit(e: any) {
      e.preventDefault()
      this.loading = true
      this.error = false

      try {
        const monster = await this.$axios(
          `https://api.osrsbox.com/monsters?where={ "name": "${this.formattedMonsterName}", "duplicate": false }`
        )
        this.monster = monster.data._items
        this.loading = false
      } catch (error) {
        console.error(error)
        this.error = true
      }
    },
  },
})
</script>

<style lang="scss">
</style>
