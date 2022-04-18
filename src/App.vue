<template>
  <v-app theme="light">
    <v-app-bar app color="primary">
      <v-app-bar-nav-icon @click="drawer=!drawer"></v-app-bar-nav-icon>
      <v-app-bar-title>CatchUp</v-app-bar-title>
    </v-app-bar>
    <side-menu :drawer="drawer" v-on:source-selected="setSource"></side-menu>
    <v-main>
      <v-container fluid>
        <unavailable-content v-if="errors.count > 0" :errors="errors"/>
        <main-content v-else :articles="articles"></main-content>

      </v-container>
      <v-footer color="primary">
        <footer-content/>
      </v-footer>
    </v-main>
  </v-app>
</template>

<script>
import { NewsApiService } from "./core/services/news-api.service";
import SideMenu from "./components/side-menu.vue";
import MainContent from "./components/main-content.vue";
import UnavailableContent from "./components/unavailable-content.vue";
import FooterContent from "./components/footer-content.vue";

export default {
  name: 'App',

  components: {
    FooterContent,
    UnavailableContent,
    MainContent,
    SideMenu,
  },

  data() {
    return {
      drawer: false,
      articles: [],
      errors: [],
      newsApi: new NewsApiService()
    };
  },

  created() {
    console.log('created');
    this.getArticlesForSource('bbc-news');
  },

  methods: {

    // On Source selected
    setSource(source) {
      this.drawer = !this.drawer;
      this.getArticlesForSourceWithLogo(source);
    },

    // Fetch articles from source id
    getArticlesForSource(sourceId) {
      this.newsApi.getArticlesForSource(sourceId)
          .then(response => {
            this.articles = response.data.articles;
            console.log(response.data);
          })
          .catch(e => {
            this.errors.push(e);
          })
    },

    // Fetch articles from selected source
    getArticlesForSourceWithLogo(source) {
      this.newsApi.getArticlesForSource(source.id)
          .then(response => {
            this.articles = response.data.articles;
            this.articles.map(article => article.source.url = source.url);
          })
          .catch(e => {
            this.errors.push(e);
          })
    }
  }
}
</script>
