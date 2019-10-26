<template>
	<v-container class="home">
		<v-row justify="center">
			<v-col cols="12">
				<h1 class="display-3 text-center">Welcome to BEERS!</h1>
			</v-col>
		</v-row>
		<v-row>
			<v-col cols="12">
				<BeerList></BeerList>
			</v-col>
		</v-row>
	</v-container>
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
