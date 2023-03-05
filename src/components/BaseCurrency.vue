<template lang="pug">
div.card.wrapper(v-on:click="toggleBase")
  div.symbol {{symbol}}
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class BaseCurrency extends Vue {
  @Prop() symbol!: string;

  toggleBase() {
    this.$emit("base-change", this.$props.symbol === "USD" ? "EUR" : "USD");
  }
}
</script>

<style scoped>
.wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 8rem;
  height: 4rem;
}

.wrapper:hover {
  cursor: pointer;
}

.symbol {
  font-size: 1.5rem;
  padding-left: 0.2rem;
}
</style>
