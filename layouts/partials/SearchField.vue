<template>
  <div>
    <v-text-field
      v-model="searchInput"
      label="Pesquisar Personagem"
      @keyup.enter.native="getCharacters"
    >
      <template slot="append">
        <v-icon v-if="hasText" @click="clearButton">clear</v-icon>
      </template>
      <template slot="append-outer">
        <v-icon @click="getCharacters">search</v-icon>
      </template>
    </v-text-field>
    <p>{{ marvelError }}</p>
    <ul v-for="character in characters" :key="character.id">
      <li>
        {{ character.thumbnail.path }}
      </li>
      <li>
        {{ character.name }}
      </li>
      <li v-if="character.description != ''">
        {{ character.description }}
      </li>
    </ul>
  </div>
</template>

<script>
import { private_key, public_key } from '~/marvel'
import md5 from 'blueimp-md5'
import _ from 'lodash'

export default {
  data() {
    return {
      searchInput: '',
      characters: [],
      marvelError: 'Pesquise uma personagem da marvel.'
    }
  },
  computed: {
    hasText() {
      return this.searchInput.length
    }
  },
  watch: {
    searchInput() {
      if (this.searchInput != '') {
        this.marvelError = 'Esperando você terminar de digitar...'
      } else {
        this.marvelError = 'Pesquise uma personagem da marvel.'
      }
      this.debouncedGetCharacters()
    }
  },
  created() {
    this.debouncedGetCharacters = _.debounce(this.getCharacters, 750)
  },
  methods: {
    clearButton() {
      this.searchInput = ''
    },
    getCharacters() {
      if (this.searchInput == '') return
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
          if (result.data.results.length == 0) {
            this.characters = []
            this.marvelError = 'Nenhuma personagem encontrada com essas letras.'
          } else {
            this.characters = result.data.results
            result.data.results.length == 1
              ? (this.marvelError = 'Personagem encontrada.')
              : (this.marvelError = 'Personagens encontradas.')
          }
        })
        .catch(error => {
          this.marvelError = error
        })
    }
  }
}
</script>

<style lang="stylus" scoped></style>
