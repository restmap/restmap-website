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
        <v-row class="ml-2 primary--text">restmap string</v-row>
        <v-row style="width: 100%" class="mt-4">
          <v-card class="rounded-lg" style="width: 100%">
            <v-text-field v-model="restmapInput" flat solo />
          </v-card>
        </v-row>

        <!--data-->
        <v-row class="mt-8 ml-2 primary--text">data</v-row>
        <v-row class="mt-4" style="width: 100%">
          <v-card class="rounded-lg" style="width: 100%">
            <v-textarea v-model="data" rows="20" flat solo />
          </v-card>
        </v-row>
      </v-col>

      <!--actions-->
      <v-col cols="1" align="center" class="mt-16">
        <v-btn fab @click="minimise" color="primary">
          <v-icon>mdi-chevron-double-right</v-icon>
        </v-btn>
      </v-col>

      <!--right area-->
      <v-col cols="5">
        <v-row class="ml-2 primary--text">output</v-row>
        <v-row style="width: 100%" class="mt-4">
          <v-card class="rounded-lg" style="width: 100%">
            <v-textarea readonly rows="25" flat solo :value="output" />
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
            <v-textarea v-model="input" rows="20" flat solo />
          </v-card>
        </v-row>
      </v-col>

      <!--action-->
      <v-col cols="1" align="center" class="mt-16">
        <v-btn fab @click="generate">
          <v-icon>mdi-chevron-double-right</v-icon>
        </v-btn>
      </v-col>

      <!--right area-->
      <v-col cols="5">
        <v-row class="ml-2">output</v-row>
        <v-row style="width: 100%" class="mt-4">
          <v-card class="rounded-lg" style="width: 100%">
            <v-text-field readonly flat solo :value="this.restmapOutput" />
          </v-card>
        </v-row>
      </v-col>
    </v-row>
  </v-container>
</template>

<script lang="ts">
import { Component, Vue, Watch } from "vue-property-decorator";
import { reduceData, generateMap, verifyMap } from "@restmap/node";

@Component({})
export default class Playground extends Vue {
  reduce = true;
  restmapInput = "{rest{query{-lang,-map,something{good}}}}";
  restmapOutput = "";
  input = "";
  data = JSON.stringify(
    {
      rest: {
        query: {
          lang: "",
          map: "",
          name: "",
          age: 2,
          something: { good: true, is: true, here: true },
        },
      },
    },
    null,
    4
  );
  output = "";

  minimise() {
    // validate restmap
    if (verifyMap(this.restmapInput)) {
      // validate data
      try {
        const data = JSON.parse(this.data);
        this.output = JSON.stringify(
          reduceData(this.restmapInput, data),
          null,
          4
        );
      } catch (e) {
        alert("invalid data (not a JSON)");
      }
    } else alert("invalid restmap");
  }

  generate() {
    //valid input
    try {
      const input = JSON.parse(this.input);
      this.restmapOutput = generateMap(input);
    } catch (e) {
      alert("kindly provide a valid JSON input");
    }
  }
}
</script>

<style scoped></style>
