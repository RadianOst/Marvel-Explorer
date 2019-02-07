<template>
  <v-app>
    <SearchBar @search="updateResultList($event)"></SearchBar>
    <ComicItem :comic="exampleComicData"></ComicItem>
    <CharacterItem :character="exampleData"></CharacterItem>
  </v-app>
</template>

<script>
import SearchBar from "./components/SearchBar";
import CharacterItem from "./components/CharacterItem";
import ComicItem from "@/components/ComicItem";

export default {
  name: 'App',
  components: {
      ComicItem,
    CharacterItem,
    SearchBar,
  },
  data () {
    return {
      searchObject: {},
      exampleList: [1, 2, 3],
      exampleComicData: {
          "id": 59551,
          "digitalId": 0,
          "title": "Spider-Man (2016) #6 (Anka Mighty Men Variant)",
          "issueNumber": 6,
          "variantDescription": "Anka Mighty Men Variant",
          "description": null,
          "modified": "2016-07-21T17:22:23-0400",
          "isbn": "",
          "upc": "75960608314500621",
          "diamondCode": "",
          "ean": "",
          "issn": "",
          "format": "Comic",
          "pageCount": 32,
          "textObjects": [],
          "resourceURI": "http://gateway.marvel.com/v1/public/comics/59551",
          "urls": [
              {
                  "type": "detail",
                  "url": "http://marvel.com/comics/issue/59551/spider-man_2016_6_anka_mighty_men_variant/anka_mighty_men_variant?utm_campaign=apiRef&utm_source=62a916d25516dbb33f8fce24264813e2"
              }
          ],
          "series": {
              "resourceURI": "http://gateway.marvel.com/v1/public/series/20508",
              "name": "Spider-Man (2016 - 2018)"
          },
          "variants": [
              {
                  "resourceURI": "http://gateway.marvel.com/v1/public/comics/55700",
                  "name": "Spider-Man (2016) #6"
              }
          ],
          "collections": [],
          "collectedIssues": [],
          "dates": [
              {
                  "type": "onsaleDate",
                  "date": "2029-12-31T00:00:00-0500"
              },
              {
                  "type": "focDate",
                  "date": "2016-07-13T00:00:00-0400"
              }
          ],
          "prices": [
              {
                  "type": "printPrice",
                  "price": 3.99
              }
          ],
          "thumbnail": {
              "path": "http://i.annihil.us/u/prod/marvel/i/mg/b/40/image_not_available",
              "extension": "jpg"
          },
          "images": [
              {
                  "path": "http://i.annihil.us/u/prod/marvel/i/mg/a/30/56f46483efc4f",
                  "extension": "jpg"
              }
          ],
          "creators": {
              "available": 2,
              "collectionURI": "http://gateway.marvel.com/v1/public/comics/59551/creators",
              "items": [
                  {
                      "resourceURI": "http://gateway.marvel.com/v1/public/creators/11575",
                      "name": "Kris Anka",
                      "role": "penciller (cover)"
                  },
                  {
                      "resourceURI": "http://gateway.marvel.com/v1/public/creators/4300",
                      "name": "Nick Lowe",
                      "role": "editor"
                  }
              ],
              "returned": 2
          },
          "characters": {
              "available": 0,
              "collectionURI": "http://gateway.marvel.com/v1/public/comics/59551/characters",
              "items": [],
              "returned": 0
          },
          "stories": {
              "available": 2,
              "collectionURI": "http://gateway.marvel.com/v1/public/comics/59551/stories",
              "items": [
                  {
                      "resourceURI": "http://gateway.marvel.com/v1/public/stories/129608",
                      "name": "cover from Spider-Man (2016) #6 (ANKA MOP VARIANT)",
                      "type": "cover"
                  },
                  {
                      "resourceURI": "http://gateway.marvel.com/v1/public/stories/129609",
                      "name": "story from Spider-Man (2016) #6 (ANKA MOP VARIANT)",
                      "type": "interiorStory"
                  }
              ],
              "returned": 2
          },
          "events": {
              "available": 0,
              "collectionURI": "http://gateway.marvel.com/v1/public/comics/59551/events",
              "items": [],
              "returned": 0
          }
      },
      exampleData: {
        "id": 1011334,
        "name": "3-D Man",
        "description": "",
        "modified": "2014-04-29T14:18:17-0400",
        "thumbnail": {
          "path": "http://i.annihil.us/u/prod/marvel/i/mg/c/e0/535fecbbb9784",
          "extension": "jpg"
        },
        "resourceURI": "http://gateway.marvel.com/v1/public/characters/1011334",
        "comics": {
          "available": 12,
          "collectionURI": "http://gateway.marvel.com/v1/public/characters/1011334/comics",
          "items": [
            {
              "resourceURI": "http://gateway.marvel.com/v1/public/comics/21366",
              "name": "Avengers: The Initiative (2007) #14"
            },
            {
              "resourceURI": "http://gateway.marvel.com/v1/public/comics/24571",
              "name": "Avengers: The Initiative (2007) #14 (SPOTLIGHT VARIANT)"
            },
            {
              "resourceURI": "http://gateway.marvel.com/v1/public/comics/21546",
              "name": "Avengers: The Initiative (2007) #15"
            },
            {
              "resourceURI": "http://gateway.marvel.com/v1/public/comics/21741",
              "name": "Avengers: The Initiative (2007) #16"
            },
            {
              "resourceURI": "http://gateway.marvel.com/v1/public/comics/21975",
              "name": "Avengers: The Initiative (2007) #17"
            },
            {
              "resourceURI": "http://gateway.marvel.com/v1/public/comics/22299",
              "name": "Avengers: The Initiative (2007) #18"
            },
            {
              "resourceURI": "http://gateway.marvel.com/v1/public/comics/22300",
              "name": "Avengers: The Initiative (2007) #18 (ZOMBIE VARIANT)"
            },
            {
              "resourceURI": "http://gateway.marvel.com/v1/public/comics/22506",
              "name": "Avengers: The Initiative (2007) #19"
            },
            {
              "resourceURI": "http://gateway.marvel.com/v1/public/comics/8500",
              "name": "Deadpool (1997) #44"
            },
            {
              "resourceURI": "http://gateway.marvel.com/v1/public/comics/10223",
              "name": "Marvel Premiere (1972) #35"
            },
            {
              "resourceURI": "http://gateway.marvel.com/v1/public/comics/10224",
              "name": "Marvel Premiere (1972) #36"
            },
            {
              "resourceURI": "http://gateway.marvel.com/v1/public/comics/10225",
              "name": "Marvel Premiere (1972) #37"
            }
          ],
          "returned": 12
        },
        "series": {
          "available": 3,
          "collectionURI": "http://gateway.marvel.com/v1/public/characters/1011334/series",
          "items": [
            {
              "resourceURI": "http://gateway.marvel.com/v1/public/series/1945",
              "name": "Avengers: The Initiative (2007 - 2010)"
            },
            {
              "resourceURI": "http://gateway.marvel.com/v1/public/series/2005",
              "name": "Deadpool (1997 - 2002)"
            },
            {
              "resourceURI": "http://gateway.marvel.com/v1/public/series/2045",
              "name": "Marvel Premiere (1972 - 1981)"
            }
          ],
          "returned": 3
        },
        "stories": {
          "available": 21,
          "collectionURI": "http://gateway.marvel.com/v1/public/characters/1011334/stories",
          "items": [
            {
              "resourceURI": "http://gateway.marvel.com/v1/public/stories/19947",
              "name": "Cover #19947",
              "type": "cover"
            },
            {
              "resourceURI": "http://gateway.marvel.com/v1/public/stories/19948",
              "name": "The 3-D Man!",
              "type": "interiorStory"
            },
            {
              "resourceURI": "http://gateway.marvel.com/v1/public/stories/19949",
              "name": "Cover #19949",
              "type": "cover"
            },
            {
              "resourceURI": "http://gateway.marvel.com/v1/public/stories/19950",
              "name": "The Devil's Music!",
              "type": "interiorStory"
            },
            {
              "resourceURI": "http://gateway.marvel.com/v1/public/stories/19951",
              "name": "Cover #19951",
              "type": "cover"
            },
            {
              "resourceURI": "http://gateway.marvel.com/v1/public/stories/19952",
              "name": "Code-Name:  The Cold Warrior!",
              "type": "interiorStory"
            },
            {
              "resourceURI": "http://gateway.marvel.com/v1/public/stories/47184",
              "name": "AVENGERS: THE INITIATIVE (2007) #14",
              "type": "cover"
            },
            {
              "resourceURI": "http://gateway.marvel.com/v1/public/stories/47185",
              "name": "Avengers: The Initiative (2007) #14 - Int",
              "type": "interiorStory"
            },
            {
              "resourceURI": "http://gateway.marvel.com/v1/public/stories/47498",
              "name": "AVENGERS: THE INITIATIVE (2007) #15",
              "type": "cover"
            },
            {
              "resourceURI": "http://gateway.marvel.com/v1/public/stories/47499",
              "name": "Avengers: The Initiative (2007) #15 - Int",
              "type": "interiorStory"
            },
            {
              "resourceURI": "http://gateway.marvel.com/v1/public/stories/47792",
              "name": "AVENGERS: THE INITIATIVE (2007) #16",
              "type": "cover"
            },
            {
              "resourceURI": "http://gateway.marvel.com/v1/public/stories/47793",
              "name": "Avengers: The Initiative (2007) #16 - Int",
              "type": "interiorStory"
            },
            {
              "resourceURI": "http://gateway.marvel.com/v1/public/stories/48361",
              "name": "AVENGERS: THE INITIATIVE (2007) #17",
              "type": "cover"
            },
            {
              "resourceURI": "http://gateway.marvel.com/v1/public/stories/48362",
              "name": "Avengers: The Initiative (2007) #17 - Int",
              "type": "interiorStory"
            },
            {
              "resourceURI": "http://gateway.marvel.com/v1/public/stories/49103",
              "name": "AVENGERS: THE INITIATIVE (2007) #18",
              "type": "cover"
            },
            {
              "resourceURI": "http://gateway.marvel.com/v1/public/stories/49104",
              "name": "Avengers: The Initiative (2007) #18 - Int",
              "type": "interiorStory"
            },
            {
              "resourceURI": "http://gateway.marvel.com/v1/public/stories/49106",
              "name": "Avengers: The Initiative (2007) #18, Zombie Variant - Int",
              "type": "interiorStory"
            },
            {
              "resourceURI": "http://gateway.marvel.com/v1/public/stories/49888",
              "name": "AVENGERS: THE INITIATIVE (2007) #19",
              "type": "cover"
            },
            {
              "resourceURI": "http://gateway.marvel.com/v1/public/stories/49889",
              "name": "Avengers: The Initiative (2007) #19 - Int",
              "type": "interiorStory"
            },
            {
              "resourceURI": "http://gateway.marvel.com/v1/public/stories/54371",
              "name": "Avengers: The Initiative (2007) #14, Spotlight Variant - Int",
              "type": "interiorStory"
            }
          ],
          "returned": 20
        },
        "events": {
          "available": 1,
          "collectionURI": "http://gateway.marvel.com/v1/public/characters/1011334/events",
          "items": [
            {
              "resourceURI": "http://gateway.marvel.com/v1/public/events/269",
              "name": "Secret Invasion"
            }
          ],
          "returned": 1
        },
        "urls": [
          {
            "type": "detail",
            "url": "http://marvel.com/characters/74/3-d_man?utm_campaign=apiRef&utm_source=62a916d25516dbb33f8fce24264813e2"
          },
          {
            "type": "wiki",
            "url": "http://marvel.com/universe/3-D_Man_(Chandler)?utm_campaign=apiRef&utm_source=62a916d25516dbb33f8fce24264813e2"
          },
          {
            "type": "comiclink",
            "url": "http://marvel.com/comics/characters/1011334/3-d_man?utm_campaign=apiRef&utm_source=62a916d25516dbb33f8fce24264813e2"
          }
        ]
      }
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
