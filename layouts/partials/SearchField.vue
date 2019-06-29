<template>
  <v-text-field v-model="searchInput" label="Pesquisar Personagem">
    <template slot="append">
      <v-icon v-if="hasText" @click="clearButton">clear</v-icon>
    </template>
    <template slot="append-outer">
      <v-icon>search</v-icon>
    </template>
  </v-text-field>
</template>

<script>
export default {
  data() {
    return {
      searchInput: ''
    }
  },
  computed: {
    hasText() {
      return this.searchInput.length
    }
  },
  methods: {
    clearButton() {
      this.searchInput = ''
    }
  }
}
</script>

<style lang="stylus" scoped></style>
