<template>
  <v-container>
    <!--buttons-->
    <v-row justify="center" class="mt-8">
      <v-col cols="auto">
        <v-btn color="primary" :outlined="!reduce" @click="reduce = true">
          Reduce
        </v-btn>

        <v-btn
          color="primary"
          class="ml-8"
          :outlined="reduce"
          @click="reduce = false"
        >
          Generate
        </v-btn>
      </v-col>
    </v-row>

    <!--reduce-->
    <v-row class="mt-12" v-if="reduce">
      <!--left area-->
      <v-col cols="6">
        <!--restmap-->
        <v-row class="ml-2">restmap string</v-row>
        <v-row style="width: 100%" class="mt-4">
          <v-card class="rounded-lg" style="width: 100%">
            <v-text-field flat solo />
          </v-card>
        </v-row>

        <!--input-->
        <v-row class="mt-8 ml-2">data</v-row>
        <v-row class="mt-4" style="width: 100%">
          <v-card class="rounded-lg" style="width: 100%">
            <v-textarea rows="20" flat solo />
          </v-card>
        </v-row>
      </v-col>

      <v-col cols="1" align="center" class="mt-16">
        <v-btn fab>
          <v-icon>mdi-chevron-double-right</v-icon>
        </v-btn>
      </v-col>

      <!--right area-->
      <v-col cols="5">
        <v-row class="ml-2">output</v-row>
        <v-row style="width: 100%" class="mt-4">
          <v-card class="rounded-lg" style="width: 100%">
            <v-textarea disabled rows="25" flat solo value="Hello" />
          </v-card>
        </v-row>
      </v-col>
    </v-row>

    <!--generate-->
    <v-row class="mt-12" v-else>
      <!--left area-->
      <v-col cols="6">
        <!--input-->
        <v-row class="ml-2">data</v-row>
        <v-row class="mt-4" style="width: 100%">
          <v-card class="rounded-lg" style="width: 100%">
            <v-textarea rows="20" flat solo />
          </v-card>
        </v-row>
      </v-col>

      <v-col cols="1" align="center" class="mt-16">
        <v-btn fab>
          <v-icon>mdi-chevron-double-right</v-icon>
        </v-btn>
      </v-col>

      <!--right area-->
      <v-col cols="5">
        <v-row class="ml-2">output</v-row>
        <v-row style="width: 100%" class="mt-4">
          <v-card class="rounded-lg" style="width: 100%">
            <v-text-field disabled flat solo value="Hello" />
          </v-card>
        </v-row>
      </v-col>
    </v-row>
  </v-container>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

@Component({})
export default class Playground extends Vue {
  reduce = false;
}
</script>

<style scoped></style>
