<template>
  <div>
    <v-text-field v-model="searchInput" label="Pesquisar Personagem">
      <template slot="append">
        <v-icon v-if="hasText" @click="clearButton">clear</v-icon>
      </template>
      <template slot="append-outer">
        <v-icon @click="getCharacters">search</v-icon>
      </template>
    </v-text-field>
    <span>{{ characters }}</span>
  </div>
</template>

<script>
import { private_key, public_key } from '~/marvel'
import md5 from 'blueimp-md5'

export default {
  data() {
    return {
      searchInput: '',
      characters: []
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
    },
    getCharacters() {
      this.$axios
        .$get(
          'http://gateway.marvel.com/v1/public/characters?nameStartsWith=' +
            this.searchInput +
            '&orderBy=name&ts=' +
            this.$moment().format() +
            '&apikey=' +
            public_key +
            '&hash=' +
            md5(this.$moment().format() + private_key + public_key)
        )
        .then(result => {
          console.log(result.data.results)
          this.characters = result.data.results
        })
        .catch(error => {
          console.log(error)
        })
    }
  }
}
</script>

<style lang="stylus" scoped></style>
