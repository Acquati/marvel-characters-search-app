<template>
  <div>
    <v-container class="p-0">
      <v-layout justify-center row>
        <v-flex xs12 sm6>
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
        </v-flex>
      </v-layout>
    </v-container>
    <v-container fluid grid-list-md>
      <v-layout justify-center row wrap>
        <v-flex
          v-for="character in characters"
          :key="character.id"
          xs12
          sm6
          md4
        >
          <v-card>
            <v-img
              :src="
                character.thumbnail.path + '.' + character.thumbnail.extension
              "
              height="200px"
            ></v-img>

            <v-card-title primary-title>
              <div class="title text-truncate">{{ character.name }}</div>
            </v-card-title>

            <v-card-actions>
              <v-spacer></v-spacer>
              <v-btn darck class="white--text" color="purple">Explore</v-btn>
            </v-card-actions>
          </v-card>
        </v-flex>
      </v-layout>
    </v-container>
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
