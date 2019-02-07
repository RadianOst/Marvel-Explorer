<template>
    <v-container>
        <v-card>
            <v-container>
                <v-card-title primary-title="">
                    <div class="headline">{{ comic.title }}</div>
                </v-card-title>
                <v-layout row>
                    <v-flex>
                        <v-tabs show-arrows grow>
                            <v-tabs-slider color="orange accent-4"></v-tabs-slider>
                            <v-tab
                                    v-for="tab in tabs"
                                    :key="tab"
                            >
                                {{ tab }}
                            </v-tab>
                            <v-tab-item
                                    key="Details"
                            >
                                <v-card>
                                    <v-layout row>
                                        <v-flex shrink pa-2>
                                            <v-img
                                                    :src="imgUrl"
                                                    height="125px"
                                                    width="150px"
                                            ></v-img>
                                        </v-flex>
                                        <v-card-title primary-title>
                                            <div>
                                                <v-layout row>
                                                    <v-flex pa-2><span class="orange--text text--accent-4">Series:</span> {{ comic.series.name }}</v-flex>
                                                    <v-flex pa-2><span class="orange--text text--accent-4">Format:</span> {{ comic.format }}</v-flex>
                                                    <v-flex pa-2><span class="orange--text text--accent-4">Pages:</span> {{ comic.pageCount }}</v-flex>
                                                </v-layout>
                                                <span>{{ this.description }}</span>
                                            </div>
                                        </v-card-title>
                                    </v-layout>
                                </v-card>
                            </v-tab-item>
                            <v-tab-item
                                    key="Variants"
                            >
                                <v-list>
                                    <v-list-tile
                                            v-for="variant in comic.variants"
                                            :key="variant.name"
                                    >
                                        <v-list-tile-content>
                                            <v-list-tile-title v-text="variant.name"></v-list-tile-title>
                                        </v-list-tile-content>
                                    </v-list-tile>
                                </v-list>
                            </v-tab-item>
                            <v-tab-item
                                    key="Prices"
                            >
                                <v-list>
                                    <v-list-tile
                                            v-for="price in comic.prices"
                                            :key="price.type"
                                    >
                                        <v-list-tile-content>
                                            <v-list-tile-title v-text="`${fromCamelCase(price.type)}: $${price.price}`"></v-list-tile-title>
                                        </v-list-tile-content>
                                    </v-list-tile>
                                </v-list>
                            </v-tab-item>
                            <v-tab-item
                                    key="Creators"
                            >
                                <v-list>
                                    <v-list-tile
                                            v-for="creator in comic.creators.items"
                                            :key="creator.name"
                                    >
                                        <v-list-tile-content>
                                            <v-list-tile-title v-text="`${creator.name} - ${creator.role}`"></v-list-tile-title>
                                        </v-list-tile-content>
                                    </v-list-tile>
                                </v-list>
                            </v-tab-item>
                            <v-tab-item
                                    key="Characters"
                            >
                                <v-list>
                                    <v-list-tile
                                            v-for="character in comic.characters.items"
                                            :key="character.name"
                                    >
                                        <v-list-tile-content>
                                            <v-list-tile-title v-text="character.name"></v-list-tile-title>
                                        </v-list-tile-content>
                                    </v-list-tile>
                                </v-list>
                            </v-tab-item>
                            <v-tab-item
                                    key="Stories"
                            >
                                <v-list>
                                    <v-list-tile
                                            v-for="story in comic.stories.items"
                                            :key="story.name"
                                    >
                                        <v-list-tile-content>
                                            <v-list-tile-title v-text="`${story.name} (${story.type})`"></v-list-tile-title>
                                        </v-list-tile-content>
                                    </v-list-tile>
                                </v-list>
                            </v-tab-item>
                            <v-tab-item
                                    key="Events"
                            >
                                <v-list>
                                    <v-list-tile
                                            v-for="event in comic.events.items"
                                            :key="event.name"
                                    >
                                        <v-list-tile-content>
                                            <v-list-tile-title v-text="event.name"></v-list-tile-title>
                                        </v-list-tile-content>
                                    </v-list-tile>
                                </v-list>
                            </v-tab-item>
                            <v-tab-item
                                    key="Urls"
                            >
                                <v-list-tile
                                        v-for="url in comic.urls"
                                        :key="url.type"
                                        :href="url.url"
                                >
                                    <v-list-tile-content>
                                        <v-list-tile-title
                                                v-text="url.type"
                                                class="blue--text darken-2--text"
                                        ></v-list-tile-title>
                                    </v-list-tile-content>
                                </v-list-tile>
                            </v-tab-item>
                        </v-tabs>
                    </v-flex>
                </v-layout>
            </v-container>
        </v-card>
    </v-container>
</template>

<script>
    export default {
        name: "ComicItem",
        props: ['comic'],
        data: function() {
            return {
                tabs: ["Details", "Variants", "Prices", "Creators", "Characters", "Stories", "Events", "Urls"]
            }
        },
        computed: {
            imgUrl: function() {
                const thumbnail = this.comic.thumbnail;
                if (thumbnail) {
                    return `${thumbnail.path}.${thumbnail.extension}`;
                }
                return "@/assets/No_image_available.png";
            },
            description: function () {
                if (this.comic.description) {
                    return this.comic.description;
                }
                return "No description added.";
            }
        },
        methods: {
            fromCamelCase: function (camelCase) {
                let result = camelCase.split('');
                for (let i = 0; i < result.length; i++) {
                    let currentCharacter = result[i];
                    if (currentCharacter == currentCharacter.toUpperCase()) {
                        result.splice(i, 0, ' ');
                        result.splice(i + 1, 1, currentCharacter.toLowerCase());
                    }
                }
                return result.join('');
            }
        }
    }
</script>

<style scoped>

</style>