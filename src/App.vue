<template>
  <v-app>
    <SearchBar @search="setSearchObject($event)"></SearchBar>
    <CharacterItem v-for="item in result" :key="item.id" :character="item"></CharacterItem>
    <BottomNavigation @change-offset="changeOffset($event)" :pagination="pagination"></BottomNavigation>

  </v-app>
</template>

<script>
import SearchBar from "./components/SearchBar";
import CharacterItem from "./components/CharacterItem";
import axios from "axios";
import BottomNavigation from "./components/BottomNavigation";

export default {
  name: 'App',
  components: {
    BottomNavigation,
    CharacterItem,
    SearchBar,
  },
  data () {
    return {
      apiKey: '62a916d25516dbb33f8fce24264813e2',
      baseUrl: 'https://gateway.marvel.com:443/v1/public/',
      searchObject: {},
      result: [],
        pagination: {
          offset: 0,
          limit: 0,
          totalItems: 0,
          description: 'page 0 - 0 of 0'
        }
    }
  },
  methods: {
    setSearchObject(searchObject) {
      this.searchObject = searchObject;
      this.pagination.limit = searchObject.limit;
      this.pagination.offset = 0;

      this.updateResultList()
    },
    changeOffset(increment) {
      if (increment) {
        this.pagination.offset += this.searchObject.limit
      } else {
        this.pagination.offset -= this.searchObject.limit
      }

      this.updateResultList()
    },
    updateResultList() {
      axios.get(`${this.baseUrl}${this.category}${this.searchObject.text}&orderBy=${this.searchObject.order}&limit=${this.searchObject.limit}&offset=${this.pagination.offset}&apikey=${this.apiKey}`)
        .then(response => {
            this.pagination.totalItems = response.data.data.total;
            this.pagination.description = `page ${this.pagination.offset + 1} - ${this.pagination.offset + this.searchObject.limit} of ${this.pagination.totalItems}`;
            this.result = response.data.data.results
        })
        .catch(err => this.console.err(err))
    }
  },
  computed: {
    category() {
      let category = '';
      switch (this.searchObject.category) {
        case 'comics':
          category = 'comics?titleStartsWith=';
          break;
        case 'characters':
          category = 'characters?nameStartsWith=';
          break;
        case 'series':
          category = 'series?titleStartsWith=';
          break;
      }
      return category;
    }
  }
}
</script>
