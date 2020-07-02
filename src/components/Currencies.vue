<template>
  <div>
    <Currency v-for="(rate, index) in rates" v-bind:value="rate" :key="index" />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

import Currency from "./Currency.vue";

@Component({
  components: {
    Currency
  }
})
export default class Currencies extends Vue {
  private rates: Array<{ [currency: string]: number }> = [];
  private symbols: string[] = ["USD", "GBP"];

  mounted() {
    fetch(
      `https://api.exchangeratesapi.io/latest?symbols=${this.symbols.join()}`
    )
      .then(stream => stream.json())
      .then(data => (this.rates = data.rates));
  }
}
</script>

<style scoped></style>
