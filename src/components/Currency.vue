<template lang="pug">
    div.wrapper
      div {{value}}
        span.symbol {{symbol}}
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class Currencies extends Vue {
  @Prop() value!: string;
  @Prop() symbol!: string;
}
</script>

<style scoped>
.wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
  background: #000;
  border-radius: 4px;
  color: white;
  font-size: 2rem;
  font-weight: 600;
  box-shadow: 0px 0px 6px 0px rgba(0, 0, 0, 1);
}

.symbol {
  font-size: 1.5rem;
  padding-left: 0.2rem;
}
</style>
