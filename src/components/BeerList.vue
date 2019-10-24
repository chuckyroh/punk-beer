<template>
	<div class="beers">
		<h2>Page: {{ page }}</h2>
		<div>
			<button @click="goPrevPage" v-show="this.page > 1">Prev</button>
			<button @click="goNextPage">Next</button>
		</div>
		<ul>
			<li v-for="beer in beers" :key="beer.id">
				<img :src="beer.image_url">
				<h3>{{ beer.name }} - <small>{{ beer.tagline }}</small></h3>
			</li>
		</ul>
	</div>
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
