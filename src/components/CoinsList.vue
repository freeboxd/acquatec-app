<template>
	<div class="col-sm">
		<div class="card">
			<div class="card-body">
				<input type="text" class="form-control" v-model="searchQuery" placeholder="Search for a coin">
				<br>
				<div class="movielist">
					<table class="table table-sm table-hover">
					  <tbody>
					    <!-- <tr class="table-primary"> -->
					    <tr v-for="coin in FilteredCoins">
					      <td><a href="#">{{coin.name}} ({{coin.symbol}})</a></td>
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

@Component
export default class HelloWorld extends Vue {
  private searchQuery: string = '';
  @Prop() private info!: any[];
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