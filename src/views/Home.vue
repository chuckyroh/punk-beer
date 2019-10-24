<template>
	<div class="home">
		<h1>Welcome to BEERS!</h1>
		<BeerList></BeerList>
	</div>
</template>

<script>
// @ is an alias to /src
import BeerList from '@/components/BeerList.vue'

export default {
	name: 'home',
	components: {
		BeerList
	}
}
</script>
