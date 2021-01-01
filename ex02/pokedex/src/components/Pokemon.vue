<template>
<div>
	{{poke_url}}
</div>
</template>

<script>
// import axios from 'axios'

export default {
	props: {poke_url: {type: Object}},
	data: function () {
		return {}
	},
	methods: {},
	mounted: function () {
		console.log(this.poke_url);
	}
}
</script>
