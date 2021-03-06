<template>
  <v-toolbar
    color="orange accent-1"
    prominent
    tabs
  >
    <v-toolbar-side-icon></v-toolbar-side-icon>
    <v-toolbar-title class="title mr-4">Cryptocurrency</v-toolbar-title>
    <v-autocomplete
      v-model="model"
      :items="items"
      :loading="isLoading"
      :search-input.sync="search"
      chips
      clearable
      hide-details
      hide-selected
      item-text="name"
      item-value="symbol"
      label="Search for a coin..."
      solo
    >
      <template slot="no-data">
        <v-list-tile>
          <v-list-tile-title>
            Search for your favorite
            <strong>Cryptocurrency</strong>
          </v-list-tile-title>
        </v-list-tile>
      </template>
      <template
        slot="selection"
        slot-scope="{ item, selected }"
      >
        <v-chip
          color="blue-grey"
          class="white--text"
          :selected="selected"
        >
          <v-icon left>mdi-coin</v-icon>
          <span v-text="item.name"></span>
        </v-chip>
      </template>
      <template
        slot="item"
        slot-scope="{ item, tile }"
      >
        <v-list-tile-avatar
          color="indigo"
          class="headline font-weight-light white--text"
        >
          {{ item.name.charAt(0) }}
        </v-list-tile-avatar>
        <v-list-tile-content>
          <v-list-tile-title v-text="item.name"></v-list-tile-title>
          <v-list-tile-sub-title v-text="item.symbol"></v-list-tile-sub-title>
        </v-list-tile-content>
        <v-list-tile-action>
          <v-icon>mdi-coin</v-icon>
        </v-list-tile-action>
      </template>
    </v-autocomplete>
    <v-tabs
      :hide-slider="!model"
      color="transparent"
      slot="extension"
      slider-color="blue-grey"
    >
      <v-tab :disabled="!model">News</v-tab>
      <v-tab :disabled="!model">Trading</v-tab>
      <v-tab :disabled="!model">Blog</v-tab>
    </v-tabs>
  </v-toolbar>
</template>

<script>
  export default {
    data: () => ({
      isLoading: false,
      items: [],
      model: null,
      search: null
    }),

    watch: {
      search (val) {
        // Items have already been loaded
        if (this.items.length > 0) return

        this.isLoading = true

        // Lazily load input items
        window.axios.get('https://api.coinmarketcap.com/v2/listings/')
          .then(res => {
            this.items = res.data.data
          })
          .catch(err => {
            console.log(err)
          })
          .finally(() => (this.isLoading = false))
      }
    }
  }
</script>

<codepen-resources lang="json">
  {
    "js": ["https://cdn.jsdelivr.net/npm/axios@0.18.0/dist/axios.min.js"]
  }
</codepen-resources>
