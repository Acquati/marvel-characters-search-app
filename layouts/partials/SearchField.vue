<template>
  <div>
    <v-text-field
      v-model="searchText"
      label="Search Character"
      @keyup.enter.native="fetchCharacters"
    >
      <template slot="append">
        <v-icon v-if="hasText" @click="clearButton">clear</v-icon>
      </template>
      <template slot="append-outer">
        <v-icon @click="fetchCharacters">search</v-icon>
      </template>
    </v-text-field>
    <p>{{ answer }}</p>
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
      searchText: '',
      characters: [],
      answer: 'Search for a Marvel character.'
    }
  },
  computed: {
    hasText() {
      return this.searchText.length
    }
  },
  watch: {
    searchText() {
      if (this.searchText != '') {
        this.answer = 'Waiting for you to finish typing ...'
      } else {
        this.answer = 'Search for a Marvel character.'
      }
      this.debouncedFetchCharacters()
    }
  },
  created() {
    this.debouncedFetchCharacters = _.debounce(this.fetchCharacters, 500)
  },
  methods: {
    clearButton() {
      this.searchText = ''
    },
    fetchCharacters() {
      if (this.searchText == '') return
      this.$axios
        .$get(
          'http://gateway.marvel.com/v1/public/characters?nameStartsWith=' +
            this.searchText +
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
            this.answer = 'No character found with these letters.'
          } else {
            this.characters = result.data.results
            result.data.results.length == 1
              ? (this.answer = 'Character found.')
              : (this.answer = 'Characters found.')
          }
        })
        .catch(error => {
          this.answer = 'Marvel API: ' + error
        })
    }
  }
}
</script>

<style lang="stylus" scoped></style>
