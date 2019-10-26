<template>
	<v-row class="beers">
		<v-col cols="12">
			<v-row justify="center">
				<v-col cols="6">
					<h2 class="text-center">Page: {{ page }}</h2>
				</v-col>
			</v-row>
			<v-row justify="center">
				<v-col cols="6" class="text-center">
					<v-btn class="mx-1" @click="goPrevPage" v-show="this.page > 1">Prev</v-btn>
					<v-btn class="mx-1" @click="goNextPage">Next</v-btn>
				</v-col>
			</v-row>
			<v-row justify="center">
				<v-col cols="12">
					<v-item-group>
						<v-container>
							<v-row justify="center">
								<v-col cols="2" v-for="beer in beers" :key="beer.id">
									<v-item>
										<v-card class="pa-2 text-center" color="grey lighten-3">
											<img :src="beer.image_url">
											<p>{{ beer.name }}</p>
										</v-card>
									</v-item>
								</v-col>
							</v-row>
						</v-container>
					</v-item-group>
				</v-col>
			</v-row>
		</v-col>
	</v-row>
</template>

<script>

import axios from 'axios';

export default {
	name: 'Beers',
	data: () => ({
		beers: [],
		page: 1
	}),
	methods: {
		async getBeers (page) {
			let response = await axios.get("https://api.punkapi.com/v2/beers?page=" + page + "&per_page=80");
			return response.data;
		},
		async goPrevPage () {
			try {
				this.page--;
				let response = await this.getBeers(this.page);
				this.beers = response;
			} catch(err) {
				alert(err);
			}
		},
		async goNextPage () {
			try {
				this.page++;
				let response = await this.getBeers(this.page);
				this.beers = response;
			} catch(err) {
				alert(err);
			}
		}
	},
	created () {
		this.getBeers(1).then(beers => this.beers = beers).catch(alert);
	}
}

</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
	.beers {
		ul {
			list-style-type: none;
			padding: 0;
			margin: 0;
		}
		li {
			display: inline-block;
			padding: 10px;
			background: hsl(0, 0, 95%);
			margin: 5px;
		}
		img {
			height: 100px;
		}
	}
</style>
