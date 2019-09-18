<template>
  <div id="app">
    <section>
      <div class="container">
        <h1>Top 100 Cryptocurrency Comparison</h1>
        <div class="row">
          <CoinsList v-bind:info="info"/>
          <div class="w-100 d-lg-none"><br></div>
          <CoinsList v-bind:info="info"/>
        </div>
        <br>
        <a href="#" class="btn btn-primary">Go somewhere</a>
      </div>
    </section>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import CoinsList from './components/CoinsList.vue';
import axios from 'axios';

@Component({
  components: {
    CoinsList,
  },
})
export default class App extends Vue {
  private info: any[] = [];
  private mounted() {
    axios
      .get('https://api.coinlore.com/api/tickers/?start=0&limit=100')
      .then((response) => (this.info = response.data.data));
  }
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