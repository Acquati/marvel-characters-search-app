<template>
  <v-text-field v-model="searchInput" label="Pesquisar Personagem">
    <template slot="append">
      <v-icon @click="clearButton">clear</v-icon>
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
  methods: {
    clearButton() {
      this.searchInput = ''
    }
  }
}
</script>

<style lang="stylus" scoped></style>
