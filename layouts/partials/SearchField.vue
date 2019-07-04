<template>
  <div>
    <v-container class="pb-0">
      <v-layout justify-center row>
        <v-flex xs12 sm6>
          <v-text-field
            v-model="searchText"
            label="Search Character"
            @keyup.enter="fetchCharacters"
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
    <v-container grid-list-md>
      <v-layout row wrap>
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
            >
              <v-layout pa-1 column fill-height class="lightbox white--text">
                <v-spacer></v-spacer>
                <v-flex shrink class="pb-0">
                  <div class="pb-0 body-1 text-xs-right">
                    ©2019 MARVEL
                  </div>
                </v-flex>
              </v-layout>
            </v-img>

            <v-card-title primary-title>
              <div class="title text-truncate">{{ character.name }}</div>
            </v-card-title>

            <v-card-actions>
              <v-spacer></v-spacer>
              <CharacterModal :character="character" />
            </v-card-actions>
          </v-card>
        </v-flex>
      </v-layout>
      <CharacterPlaceholder v-if="hasCharacters == 0" />
    </v-container>
  </div>
</template>

<script>
import CharacterModal from '~/components/CharacterModal.vue'
import CharacterPlaceholder from '~/components/CharacterPlaceholder.vue'
import { private_key, public_key } from '~/marvel'
import md5 from 'blueimp-md5'
import _ from 'lodash'

export default {
  components: {
    CharacterModal,
    CharacterPlaceholder
  },
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
    },
    hasCharacters() {
      return this.characters.length
    }
  },
  watch: {
    searchText() {
      if (this.searchText != '') {
        this.answer = 'Waiting for Marvel API ...'
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
