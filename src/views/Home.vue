<template>
  <div />
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

@Component({})
export default class Home extends Vue {
  created() {
    window.location.href = "https://github.com/restmap";
  }
}
</script>
