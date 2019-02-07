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
                        <div class="headline">{{ character.name }}</div>
                    </v-card-title>
                </v-layout>
                <v-layout row>
                    <v-flex>
                        <v-tabs show-arrows grow>
                            <v-tabs-slider color="blue accent-4"></v-tabs-slider>
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
                                            v-for="comic in character.comics.items"
                                            :key="comic.resourceURI"
                                    >
                                        <v-list-tile-content>
                                            <v-list-tile-title v-text="comic.name"></v-list-tile-title>
                                        </v-list-tile-content>
                                    </v-list-tile>
                                </v-list>
                            </v-tab-item>
                            <v-tab-item
                                key="Series"
                            >
                                <v-list>
                                    <v-list-tile
                                            v-for="serie in character.series.items"
                                            :key="serie.resourceURI"
                                    >
                                        <v-list-tile-content>
                                            <v-list-tile-title v-text="serie.name"></v-list-tile-title>
                                        </v-list-tile-content>
                                    </v-list-tile>
                                </v-list>
                            </v-tab-item>
                            <v-tab-item
                                key="Stories"
                            >
                                <v-list>
                                    <v-list-tile
                                            v-for="story in character.stories.items"
                                            :key="story.resourceURI"
                                    >
                                        <v-list-tile-content>
                                            <v-list-tile-title v-text="story.name"></v-list-tile-title>
                                        </v-list-tile-content>
                                    </v-list-tile>
                                </v-list>
                            </v-tab-item>
                            <v-tab-item
                                key="Events"
                            >
                                <v-list-tile
                                        v-for="event in character.events.items"
                                        :key="event.resourceURI"
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
                                        v-for="url in character.urls"
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
        name: "CharacterItem",
        props: ['character'],
        data: function() {
            return {
                //
            }
        },
        computed: {
            imgUrl: function() {
                const thumbnail = this.character.thumbnail;
                if (thumbnail) {
                    return `${thumbnail.path}.${thumbnail.extension}`;
                }
                return "@/assets/No_image_available.png";
            },
            description: function () {
                if (this.character.description) {
                    return this.character.description;
                }
                return "No description added.";
            },
            tabs: function () {
                return [
                    'Details',
                    `Comics (${this.character.comics.available})`,
                    `Series (${this.character.series.available})`,
                    `Stories (${this.character.stories.available})`,
                    `Events (${this.character.events.available})`,
                    "Urls"
                ];
            }
        }
    }
</script>

<style scoped>

</style>