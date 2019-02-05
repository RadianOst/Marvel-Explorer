<template>
    <v-toolbar>
        <v-menu transition="slide-y-transition">
            <v-btn
                    slot="activator"
            >
                {{ selectedCategory }}
                <v-icon dark>arrow_drop_down</v-icon>
            </v-btn>
            <v-list>
                <v-list-tile
                        v-for="category in dropdownCategories"
                        :key="category"
                        @click="setCategory(category)"
                >
                    <v-list-tile-title>{{ category }}</v-list-tile-title>
                </v-list-tile>
            </v-list>
        </v-menu>
        <v-text-field
                v-model="searchText"
                label="Search"
                @keyup="searchIfEnterPressed"
        ></v-text-field>
        <v-btn icon
                @click="search"
        >
            <v-icon>search</v-icon>
        </v-btn>
    </v-toolbar>
</template>

<script>
    export default {
        name: "SearchBar",
        data: function () {
            return {
                searchText: '',
                dropdownCategories: ['Comics', 'Characters'],
                selectedCategory: 'Comics'
            }
        },
        computed: {
            searchObject: function(){
                return {
                    category: this.selectedCategory,
                    text: this.searchText
                }
            }
        },
        methods: {
            setCategory(value) {
                this.selectedCategory = value;
            },
            search() {
                this.$emit('search', this.searchObject);
                this.searchText = '';
            },
            searchIfEnterPressed(event) {
                if (event.keyCode == 13) {
                    this.search();
                }
            }
        }
    }
</script>

<style scoped>

</style>