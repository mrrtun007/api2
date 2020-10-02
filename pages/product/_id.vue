<template>
  <v-card
    class="mx-auto"
    max-width="400"
  >
    <v-list-item two-line>
      <v-list-item-content>
        <v-list-item-title class="headline">
          {{ this.$route.params.id.name }}
        </v-list-item-title>
      </v-list-item-content>
    </v-list-item>

    <v-card-text>
      <v-row align="center">
        <v-col
          class="display-3"
          cols="6"
        >
          {{ this.$route.params.id.main.temp }}&deg;
        </v-col>
      </v-row>
      {{ this.$route.params.id.weather[0].description }}
    </v-card-text>
    <v-divider />
  </v-card>
</template>
