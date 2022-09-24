<template>
  <div>
    <BaseCurrency v-bind:symbol="base" v-on:base-change="onBaseChange" />
    <div class="grid">
      <Currency
        v-for="(rate, symbol, index) in rates"
        v-bind:value="rate"
        v-bind:symbol="symbol"
        :key="index"
      />
    </div>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

import BaseCurrency from "./BaseCurrency.vue";
import Currency from "./Currency.vue";

@Component({
  components: {
    BaseCurrency,
    Currency
  }
})
export default class Currencies extends Vue {
  private rates: Array<{ [currency: string]: number }> = [];
  private symbols: string[] = ["USD", "GBP", "RUB"];
  private base = "EUR";

  mounted() {
    this.getCurrencies();
  }

  getCurrencies() {
    const headers = new Headers();
    headers.append("apikey", process.env.VUE_APP_API_KEY);

    fetch(
      `https://api.apilayer.com/exchangerates_data/latest?base=${
        this.base
      }&symbols=${this.symbols.join()}`,
      { headers }
    )
      .then(stream => stream.json())
      .then(data => (this.rates = data.rates));
  }

  onBaseChange(value: "EUR" | "USD") {
    this.base = value;
    this.getCurrencies();
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
