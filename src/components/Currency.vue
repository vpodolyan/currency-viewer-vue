<template lang="pug">
div(v-if="symbol !== base").wrapper.card
  div {{Number(value).toFixed(3)}}
    span.symbol {{symbol}}
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class Currencies extends Vue {
  @Prop() value!: string;
  @Prop() symbol!: string;
  @Prop() base!: string;
}
</script>

<style scoped>
.wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 2vw;
}

.symbol {
  font-size: 1.5rem;
  padding-left: 0.2rem;
}
</style>
