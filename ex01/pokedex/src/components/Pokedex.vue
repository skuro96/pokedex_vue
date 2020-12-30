<template>
<div>
	<div v-if="err">{{errMessage}}</div>
	<div v-else>
		<div v-if="loading">Loading...</div>
		<div v-else v-for="poke in pokemon" v-bind:key="poke.id">
			<div>{{poke.id}}</div>
			<div>{{poke.name}}</div>
			<img :src="poke.image">
		</div>
	</div>
</div>
</template>

<script>
import axios from 'axios'
export default {
	data: function () {
		return {
			pokemon: {},
			loading: true,
			err: false,
			errMessage: ''
		};
	},
	methods: {},
	mounted: async function () {
		let res = await axios.get('https://pokeapi.co/api/v2/pokemon')
		.then ((respons) => { return respons; })
		.catch ((e) => {
			this.err = true;
			this.errMessage = e.message;
			console.log(e.message);
			return ;
		});
		console.log(res);

		let result = res.data.results;
		for (let i = 0; i < result.length; i++)
		{
			let pokeInfo = await axios.get(result[i].url)
			.then ((respons) => { return respons; })
			.catch ((e) => {
				this.err = true;
				this.errMessage = e.message;
				console.log(e.message);
				return ;
			});

			let p = pokeInfo.data;
			this.pokemon[p.id] = {};
			this.pokemon[p.id].id = p.id;
			this.pokemon[p.id].name = p.name;
			this.pokemon[p.id].image = p.sprites.front_default;
		}

		console.log(this.pokemon);
		this.loading = false;
		return ;
	},
	created: {},
	computed: {}
}
</script>