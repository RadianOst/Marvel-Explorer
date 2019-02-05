<template>
  <v-app>
    <SearchBar @search="updateResultList($event)"></SearchBar>
  </v-app>
</template>

<script>
import SearchBar from "./components/SearchBar";

export default {
  name: 'App',
  components: {
    SearchBar,
  },
  data () {
    return {
      searchObject: {}
    }
  },
  methods: {
    updateResultList(searchObject) {
      this.searchObject = searchObject;

      // TODO: send GET method to API and display results
      // probably searchObject should be deleted after implementing this method
    }
  }
}
</script>
