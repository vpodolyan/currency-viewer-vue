<template lang="pug">
    div {{rates}}
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class Currencies extends Vue {
  private rates: Array<{ [currency: string]: number }> = [];

  mounted() {
    fetch("https://api.exchangeratesapi.io/latest")
      .then(stream => stream.json())
      .then(data => (this.rates = data.rates));
  }
}
</script>

<style scoped></style>
