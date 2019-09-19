<template>
	<div class="col-sm">
		<div class="card">
			<div class="card-body">
				<div class="coin-info">
					<h3 style="font-weight: bold">#{{info[currId].rank}} {{info[currId].name}} ({{info[currId].symbol}})</h3>
					<span>Price (USD): ${{info[currId].price_usd}}</span>
					<br>
					<span>{{info[currId].price_btc}} BTC</span>
				</div>
				<br>
				<input type="text" class="form-control" v-model="searchQuery" placeholder="Search for a coin">
				<br>
				<div class="movielist">
					<table class="table table-sm table-hover">
					  <tbody>
					    <tr v-for="coin in FilteredCoins">
					      <td><a href="#" v-on:click="currId=coin.rank-1" v-bind:key="coin.nameid">{{coin.name}} ({{coin.symbol}})</a></td>
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
  public currId: number = 0;

  public mounted() {
    axios
      .get('https://api.coinlore.com/api/tickers/?start=0&limit=100')
      .then((response) => (this.info = response.data.data));
      
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