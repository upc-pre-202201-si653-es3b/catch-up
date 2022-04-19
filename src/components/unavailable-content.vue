<template>
  <v-row class="flex-column text-center">
    <v-col class="text-h4">{{ $t('unavailable-news') }}</v-col>
    <v-col v-for="error in errors" class="text-h6">{{ error }}</v-col>
  </v-row>
</template>

<script>
export default {
  name: "unavailable-content",
  props: {
    errors: null
  }
}
</script>

<style scoped>

</style>
