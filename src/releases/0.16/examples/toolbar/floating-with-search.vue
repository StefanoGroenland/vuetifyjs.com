<template>
  <v-card
    img="https://s3.amazonaws.com/vuetify-docs/images/toolbar/map.jpg"
    flat
    height="300px"
    class="pa-3"
  >
    <v-toolbar
      color="white"
      floating
      dense
    >
        <v-text-field prepend-icon="search" hide-details single-line></v-text-field>
        <v-btn icon>
          <v-icon>my_location</v-icon>
        </v-btn>
        <v-btn icon>
          <v-icon>more_vert</v-icon>
        </v-btn>
    </v-toolbar>
  </v-card>
</template>
