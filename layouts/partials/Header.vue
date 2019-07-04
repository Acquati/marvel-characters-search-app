<template>
  <v-container>
    <v-layout class="header" row wrap justify-center>
      <v-flex xs12>
        <v-card>
          <v-img
            class="white--text"
            height="200px"
            src="https://wallpaperaccess.com/full/193203.jpg"
          >
            <v-layout pa-2 column fill-height class="lightbox white--text">
              <v-spacer></v-spacer>
              <v-flex shrink class="pb-0">
                <div class="pb-0 body-1 text-xs-right">
                  ©2019 MARVEL
                </div>
              </v-flex>
            </v-layout>
          </v-img>
          <v-card-actions>
            <a
              href="https://github.com/Acquati/recrutamento-fullstack"
              target="_blank"
            >
              <v-btn color="blue-grey" class="white--text">
                github
                <v-icon right dark>code</v-icon>
              </v-btn>
            </a>
          </v-card-actions>
          <v-card-actions>
            <a href="https://developer.marvel.com/" target="_blank">
              <v-btn color="red" class="white--text"
                >marvel developer
                <v-icon right dark>gavel</v-icon>
              </v-btn>
            </a>
          </v-card-actions>
          <v-card-title>
            <div>
              {{ description }}
            </div>
          </v-card-title>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      description:
        'Search the most diverse characters on Marvel Universe: women, men, organizations, alien species, deities, animals, non-corporeal entities, trans-dimensional manifestations, abstract personifications, and green amorphous blobs which occupy the Marvel Universe (and various alternate universes, timelines and altered realities therein). For example, Spider-Man.'
    }
  }
}
</script>

<style lang="stylus" scoped>
.header {
  a {
    text-decoration: none;
  }
}
</style>
