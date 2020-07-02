<template lang="pug">
    div {{value}}
</template>

<script lang="ts">
import { Component, Prop, Vue } from "vue-property-decorator";

@Component
export default class Currencies extends Vue {
  @Prop() value!: string;
}
</script>
