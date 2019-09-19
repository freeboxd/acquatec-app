<template>
	<div class="col-sm">
		<div class="card">
			<div class="card-body">
				{{currentCoin}}
				<!-- <div class="coin-info">
					<h3 style="font-weight: bold">#{{currentCoin.rank}} {{currentCoin.name}} ({{currentCoin.symbol}})</h3>
					<span>Price (USD): ${{currentCoin.price_usd}}</span>
					<br>
					<span>{{currentCoin.price_btc}} BTC</span>
				</div> -->
				<br>
				<input type="text" class="form-control" v-model="searchQuery" placeholder="Search for a coin">
				<br>
				<div class="movielist">
					<table class="table table-sm table-hover">
					  <tbody>
					    <tr v-for="coin in FilteredCoins">
					      <td><a href="#" v-on:click="setCoin(coin.id)" v-bind:key="coin.nameid">{{coin.name}} ({{coin.symbol}})</a></td>
					    </tr>
					  </tbody>
					</table>
				</div>
			</div>
		</div>
	</div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';
import axios from 'axios';

@Component
export default class CoinsList extends Vue {
  public info: any[] = [];
  public currentCoin: object = {};

  public mounted() {
    axios
      .get('https://api.coinlore.com/api/tickers/?start=0&limit=100')
      .then((response) => (this.info = response.data.data));
      this.currentCoin = Object.assign(this.info[0]);
  }

  public set setCoin(id: number) {
  	this.currentCoin = Object.assign(this.info[id]);
  }

  public searchQuery: string = '';
  public get FilteredCoins() {
    return this.info.filter((coin) => {
      return coin.name.toLowerCase().includes(this.searchQuery.toLowerCase()) + coin.symbol.toLowerCase().includes(this.searchQuery.toLowerCase());
    });
  }
}
</script>

<style scoped>
.movielist {
	text-align: left;
	min-height: 300px;
	max-height: 300px;
	overflow-y: scroll;
}
</style>