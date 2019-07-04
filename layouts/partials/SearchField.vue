<template>
  <div>
    <v-text-field
      v-model="searchInput"
      label="Search Character"
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
      marvelError: 'Search for a Marvel character.'
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
        this.marvelError = 'Waiting for you to finish typing ...'
      } else {
        this.marvelError = 'Search for a Marvel character.'
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
            this.marvelError = 'No character found with these letters.'
          } else {
            this.characters = result.data.results
            result.data.results.length == 1
              ? (this.marvelError = 'Character found.')
              : (this.marvelError = 'Characters found.')
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
