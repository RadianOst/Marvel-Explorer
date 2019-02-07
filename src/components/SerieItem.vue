<template>
    <v-container>
        <v-card>
            <v-container>
                <v-layout row>
                    <v-flex shrink pa-2>
                        <v-img
                                :src="imgUrl"
                                height="125px"
                                width="150px"
                        ></v-img>
                    </v-flex>
                    <v-card-title primary-title="">
                        <div class="headline">{{ serie.title }}</div>
                    </v-card-title>
                </v-layout>
                <v-layout row>
                    <v-flex>
                        <v-tabs show-arrows grow>
                            <v-tabs-slider color="purple accent-4"></v-tabs-slider>
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
                                        <v-card-title primary-title>
                                            <div>
                                                <v-layout row>
                                                    <v-flex pa-2><span class="purple--text text--accent-4">Start year:</span> {{ serie.startYear }}</v-flex>
                                                    <v-flex pa-2><span class="purple--text text--accent-4">End year:</span> {{ serie.endYear }}</v-flex>
                                                    <v-flex pa-2><span class="purple--text text--accent-4">Rating:</span> {{ serie.rating }}</v-flex>
                                                </v-layout>
                                                <span>{{ this.description }}</span>
                                            </div>
                                        </v-card-title>
                                    </v-layout>
                                </v-card>
                            </v-tab-item>
                            <v-tab-item
                                key="Comics"
                            >
                                <v-list>
                                    <v-list-tile
                                            v-for="comic in serie.comics.items"
                                            :key="comic.name"
                                    >
                                        <v-list-tile-content>
                                            <v-list-tile-title v-text="comic.name"></v-list-tile-title>
                                        </v-list-tile-content>
                                    </v-list-tile>
                                </v-list>
                            </v-tab-item>
                            <v-tab-item
                                key="Creators"
                            >
                                <v-list>
                                    <v-list-tile
                                            v-for="creator in serie.creators.items"
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
                                            v-for="character in serie.characters.items"
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
                                            v-for="story in serie.stories.items"
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
                                <v-list-tile
                                        v-for="event in serie.events.items"
                                        :key="event.name"
                                >
                                    <v-list-tile-content>
                                        <v-list-tile-title v-text="event.name"></v-list-tile-title>
                                    </v-list-tile-content>
                                </v-list-tile>
                            </v-tab-item>
                            <v-tab-item
                                key="Urls"
                            >
                                <v-list-tile
                                        v-for="url in serie.urls"
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
        name: "SerieItem",
        props: ['serie'],
        data: function() {
            return {
                //
            }
        },
        computed: {
            imgUrl: function() {
                const thumbnail = this.serie.thumbnail;
                if (thumbnail) {
                    return `${thumbnail.path}.${thumbnail.extension}`;
                }
                return "@/assets/No_image_available.png";
            },
            description: function () {
                if (this.serie.description) {
                    return this.serie.description;
                }
                return "No description added.";
            },
            tabs: function () {
                return [
                    'Details',
                    `Comics (${this.serie.comics.available})`,
                    `Creators (${this.serie.creators.available})`,
                    `Characters (${this.serie.characters.available})`,
                    `Stories (${this.serie.stories.available})`,
                    `Events (${this.serie.stories.available})`,
                    "Urls"
                ];
            }
        }
    }
</script>

<style scoped>

</style>