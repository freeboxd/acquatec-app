<template>
	<div class="coin-info">
		<h3 style="font-weight: bold">#{{info[currId].rank}} {{info[currId].name}} ({{info[currId].symbol}})</h3>
		<span>Price (USD): ${{info[currId].price_usd}}</span>
		<br>
		<span>{{info[currId].price_bt}} BTC</span>
	</div>
</template>

<script lang="ts">
import { Component, Prop, Vue } from 'vue-property-decorator';

@Component
export default class CoinsList extends Vue {
	@Prop() private info!: any[];
	@Prop() private currId!: number;
}
</script>