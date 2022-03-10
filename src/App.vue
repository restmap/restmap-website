<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <v-spacer />

      <span class="ls-2 h6">Playground</span>

      <v-spacer />
    </v-app-bar>

    <v-main>
      <router-view />
    </v-main>
  </v-app>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  name: "App",

  data: () => ({
    //
  }),
});
</script>
