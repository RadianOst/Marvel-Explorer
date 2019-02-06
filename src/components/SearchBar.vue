<template>
    <v-container>
        <v-toolbar :extended="isSearchingAdvanced">
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
            <v-btn icon
                   @click="toggleAdvancedSearch"
            >
                <v-icon v-show="!isSearchingAdvanced">expand_more</v-icon>
                <v-icon v-show="isSearchingAdvanced">expand_less</v-icon>
            </v-btn>
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
            <v-toolbar-title
                    v-if="isSearchingAdvanced"
                    slot="extension"
            >
                Order by:
            </v-toolbar-title>
            <v-menu
                    v-if="isSearchingAdvanced"
                    transition="slide-y-transition"
                    slot="extension"
            >
                <v-btn slot="activator">
                    {{ selectedOrder }}
                    <v-icon dark>arrow_drop_down</v-icon>
                </v-btn>
                <v-list>
                    <v-list-tile
                            v-for="order in orderOptionsForSelectedCategory"
                            :key="order"
                            @click="setOrder(order)"
                    >
                        <v-list-tile-title>{{ order }}</v-list-tile-title>
                    </v-list-tile>
                </v-list>
            </v-menu>
            <v-btn
                    v-if="isSearchingAdvanced"
                    slot="extension"
                    @click="toggleOrder"
            >
                <v-icon v-show="isOrderAscending">trending_up</v-icon>
                <v-icon v-show="!isOrderAscending">trending_down</v-icon>
            </v-btn>
            <v-toolbar-title
                    v-if="isSearchingAdvanced"
                    slot="extension"
            >
                Limit:
            </v-toolbar-title>
            <v-menu
                    v-if="isSearchingAdvanced"
                    transition="slide-y-transition"
                    slot="extension"
            >
                <v-btn slot="activator">
                    {{ selectedLimit }}
                    <v-icon dark>arrow_drop_down</v-icon>
                </v-btn>
                <v-list>
                    <v-list-tile
                            v-for="limit in limitOptions"
                            :key="limit"
                            @click="setLimit(limit)"
                    >
                        <v-list-tile-title>{{ limit }}</v-list-tile-title>
                    </v-list-tile>
                </v-list>
            </v-menu>
        </v-toolbar>
    </v-container>

</template>

<script>
    export default {
        name: "SearchBar",
        data: function () {
            return {
                searchText: '',
                dropdownCategories: ['Comics', 'Characters'],
                selectedCategory: 'comics',
                isSearchingAdvanced: false,
                orderByOptions: {
                    comics: [
                        "title", "issue number", "modified",
                    ],
                    characters: [
                        "name", "modified"
                    ]
                },
                defaultOrder: "modified",
                selectedOrder: "modified",
                isOrderAscending: true,
                limitOptions: [1, 5, 10, 15, 20],
                selectedLimit: 20
            }
        },
        computed: {
            searchObject: function(){
                let orderTrending = '';
                if (!this.isOrderAscending) {
                    orderTrending = '-';
                }
                return {
                    category: this.selectedCategory,
                    text: this.searchText.toLowerCase(),
                    order: `${orderTrending}${this.selectedOrderCamelCased}`,
                    limit: this.selectedLimit
                }
            },
            orderOptionsForSelectedCategory: function () {
                const list = this.orderByOptions[this.selectedCategory];
                if (list) {
                    return list;
                }
                return ["modified"]
            },
            selectedOrderCamelCased: function () {
                let order = this.selectedOrder;
                order = order.split('');
                for (let i = order.length - 2; i >=0; i--) {
                    if (order[i] == ' ') {
                        const letterAfterSpace = order[i + 1].toUpperCase();
                        order.splice(i, 2, letterAfterSpace);
                    }
                }
                return order.join('');
            }
        },
        methods: {
            setCategory(value) {
                this.selectedCategory = value.toLowerCase();
                this.selectedOrder = this.defaultOrder;
            },
            setLimit(limit) {
                this.selectedLimit = limit;
            },
            setOrder(order) {
                this.selectedOrder = order;
            },
            search() {
                this.$emit('search', this.searchObject);
                this.searchText = '';
            },
            searchIfEnterPressed(event) {
                if (event.keyCode == 13) {
                    this.search();
                }
            },
            toggleAdvancedSearch() {
                this.isSearchingAdvanced = !this.isSearchingAdvanced;
            },
            toggleOrder() {
                this.isOrderAscending = !this.isOrderAscending;
            }
        }
    }
</script>

<style scoped>

</style>