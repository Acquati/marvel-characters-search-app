<template>
  <v-layout row wrap>
    <v-flex xs12 sm6 md4>
      <v-card>
        <v-img
          src="https://hottopic.scene7.com/is/image/HotTopic/10525417_hi?$pdp_hero_zoom$"
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
          <div class="title text-truncate">?!</div>
        </v-card-title>

        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="red" dark>
            ?!
            <v-icon right dark>library_books</v-icon>
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-flex>
  </v-layout>
</template>

<script>
export default {}
</script>

<style lang="stylus" scoped></style>
