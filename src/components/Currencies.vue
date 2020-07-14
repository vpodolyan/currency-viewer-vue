<template>
  <div class="grid">
    <Currency
      v-for="(rate, symbol, index) in rates"
      v-bind:value="rate"
      v-bind:symbol="symbol"
      :key="index"
    />
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

<style scoped>
.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(12rem, 1fr));
  grid-gap: 2vw;
  grid-auto-rows: 1fr;
}

.grid::before {
  content: "";
  width: 0;
  padding-bottom: 100%;
  grid-row: 1 / 1;
  grid-column: 1 / 1;
}

/** Hack to hide fisrt empty column */
.grid > *:first-child {
  grid-row: 1 / 1;
  grid-column: 1 / 1;
}
</style>
