<template>
  <v-card class="ma-2 elevation-1" hover>
    <v-img class="white--text align-end" cover
           :src="article.urlToImage"
           :alt="article.title"
           gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.5)">
      <v-card-title class="ma-3 text-white" v-text="article.title"></v-card-title>
    </v-img>
    <v-card-text class="ma-2">
      {{ article.description }}
    </v-card-text>
    <v-card-actions class="ma-2">
      <v-chip v-if="article.source.url" color="primary"
              size="x-small" link
              :href="article.source.url" target="_blank">
        {{ article.source.name }}
      </v-chip>
      <v-chip v-else color="primary" size="x-small">{{ article.source.name }}</v-chip>
      <v-spacer></v-spacer>
      <v-btn icon="mdi-reddit"      class="text-red"/>
      <v-btn icon="mdi-twitter"     class="text-blue-lighten-1"/>
      <v-btn icon="mdi-facebook"    class="text-blue-darken-4"/>
      <v-btn icon="mdi-google-plus" class="text-red"/>
      <v-btn icon="mdi-linkedin"    class="text-blue-darken-4"/>
      <v-spacer></v-spacer>
      <v-btn small replace color="info" v-bind:href="article.url" target="_blank">Read More</v-btn>
    </v-card-actions>
  </v-card>
</template>

<script>
export default {
  name: "article-card",
  props: {
    article: null
  }

}
</script>

<style scoped>

</style>
