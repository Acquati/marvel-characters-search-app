<template>
  <div>
    <v-btn color="red" dark @click.stop="dialog = true">
      know more
      <v-icon right dark>library_books</v-icon>
    </v-btn>

    <v-dialog
      v-model="dialog"
      width="800px"
      :fullscreen="$vuetify.breakpoint.smAndDown"
    >
      <v-card>
        <v-img
          :src="character.thumbnail.path + '.' + character.thumbnail.extension"
          height="300px"
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

        <v-card-title class="headline" primary-title>
          {{ character.name }}
        </v-card-title>

        <v-card-text v-if="character.description">
          {{ character.description }}
        </v-card-text>
        <v-card-text v-else>
          No description for this character was found on Marvel API.
        </v-card-text>

        <v-divider></v-divider>

        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn flat @click="dialog = false">
            <v-icon right>clear</v-icon>
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </div>
</template>

<script>
export default {
  props: {
    character: {
      default: () => [],
      type: Object
    }
  },
  data() {
    return {
      dialog: false
    }
  }
}
</script>

<style lang="stylus" scoped></style>
