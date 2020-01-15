<template>
  <v-app>
    <v-content>
     <v-card class="overflow-hidden">
      <v-app-bar
        color="red darken-1"
        dark
      >
      <!--<v-app-bar-nav-icon></v-app-bar-nav-icon>-->

      <v-toolbar-title>News</v-toolbar-title>

      <v-spacer></v-spacer>

      <v-menu
        left
        bottom
      >
      
        <!--<template v-slot:activator="{ on }">
          <v-btn icon v-on="on">
            <v-icon>mdi-dots-vertical</v-icon>
          </v-btn>
        </template>

         <v-list>
          <v-list-item
            v-for="n in languages"
            :key="n.languages"
            @click="() => {
              selectedLanguage = n,
              loadArticles()
            }"
          > 
          <v-list-item-title> {{ n }}</v-list-item-title>
          </v-list-item>
        </v-list> -->
      </v-menu>
    </v-app-bar>
    <v-sheet
      id="scrolling-techniques"
      class="overflow-y-auto"
    >
      <v-container class = "content">
      <v-row>
      <ArticleTile class = "tile" v-for = "tile in articles" :key="tile.url" :title="tile.title" :image="tile.urlToImage" :author="tile.author" :description="tile.description"></ArticleTile>
      </v-row>
      </v-container>
    </v-sheet>
    </v-card>
 </v-content>
</v-app>
</template>

<script>

import ArticleTile from './components/ArticleTile.vue'
import axios from 'axios'

export default {
  name: 'App',

  components: {
    ArticleTile,
  },

  data: () => ({
    drawer: null,
    articles: [],
    selectedLanguage: 'en',
  }),
  methods: {
    loadArticles(){
      if (this.selectedLanguage === 'ru') {
        axios.get('https://newsapi.org/v2/top-headlines?country=ru&apiKey=d7f41a32c26b4bbfb596d58b1a54c766')
        .then((response) => {
        this.articles = response.data.articles
      })
      }
      if (this.selectedLanguage === 'en') {
        axios.get('https://newsapi.org/v2/top-headlines?country=us&apiKey=d7f41a32c26b4bbfb596d58b1a54c766')
        .then((response) => {
          this.articles = response.data.articles
        })
      }

      
    }
  },
  mounted() {
    this.loadArticles()
  },
  watch: {
    selectedLanguage() {
      this.loadArticles()
    }
  }

}
</script>

<style>
  .content {
    height: 1000px;
    
 }
  .tile {
    margin: 10px;
  }
</style>