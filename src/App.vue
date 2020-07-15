<template>
  <div id="app">
    <Currencies />
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import Currencies from "./components/Currencies.vue";

@Component({
  components: {
    Currencies
  }
})
export default class App extends Vue {}
</script>

<style>
body {
  background: rgb(110, 139, 101);
}

#app {
  font-family: Ubuntu, Calibri, Verdana, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 2vw;
}

.card {
  background: #222;
  border-radius: 4px;
  color: white;
  font-size: 2rem;
  font-weight: 600;
  box-shadow: 0px 0px 6px 0px rgba(0, 0, 0, 1);
}
</style>
