<template lang="html">
	<form id="sightings-form" v-on:submit.prevent="addSighting" v-model="newSighting">
		<h2>Add a Sighting</h2>
		<div class="formWrap">
			<label for="species">Species:</label>
			<input v-model="newSighting.species" type="text" id="species" required />
		</div>
		<div class="formWrap">
			<label for="location">Location:</label>
			<input v-model="newSighting.location" type="text" id="location" required />
		</div>
		<div class="formWrap">
			<label for="date">Date:</label>
			<input v-model="newSighting.date" type="date" id="date" requried />
		</div>

		<input type="submit" value="Save" id="save"/>
	</form>
</template>

<script>
import { eventBus } from '../main.js'
export default {
	name: "SightingsForm",
	data(){
		return {
			newSighting: {
				species: "",
				location: "",
				date: null
			}
		}
	},
	methods: {
		addSighting(){
			fetch('http://localhost:3000/api/sightings', {
				method: 'POST',
				body: JSON.stringify(this.newSighting),
				headers: { 'Content-Type': 'application/json' }
			})
			.then(response => response.json())
			.then(data => eventBus.$emit('sighting-added', data))
		}
	}
}
</script>

<style lang="css" scoped>
	h2 {
		margin: 10px 0;
		padding: 0;
	}
	form {
		width: 75%;
		margin: 0 auto;
		background: rgba(255, 255, 255, 0.7);
		padding: 20px;
		margin-bottom: 40px;
	}
	label {
		min-width: 100px;
		display: inline-block;
	}
	.formWrap {
		margin-bottom: 10px;
	}
</style>
