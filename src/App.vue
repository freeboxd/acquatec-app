<template>
  <div id="app">
    <section>
      <div class="container">
        <h1>Top 100 Cryptocurrency Comparison</h1>
        <div class="row">
          <CoinsList/>
          <div class="w-100 d-lg-none"><br></div>
          <CoinsList/>
        </div>
      </div>
    </section>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import CoinsList from './components/CoinsList.vue';

@Component({
  components: {
    CoinsList,
  },
})
export default class App extends Vue {
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>