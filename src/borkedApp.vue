
import { setInterval } from 'timers';
import { setInterval } from 'timers';
<template>
  <div id="borkedApp" 
		:class="sizeClass" 
		v-on:mouseover="makeMeBigger" 
		v-on:mouseleave="makeDefault"
		>
    <h1>ZIP: {{ zip }}</h1>
		<p>{{ tick }}</p>
		<!-- <button v-on:click="fetchData">Fetch</button> -->
		<h3>Weather status: {{ weatherStatus }}</h3>
		<div v-on:click="$emit('remove-me')" class="buttonContainer">
			<button class="removeComponentButton">X</button>
		</div>
  </div>
</template>

<script>
import k2f from 'kelvin-to-fahrenheit'
export default {
	name: 'borkedApp',
	props: ['zip'],
  data () {
    return {
			sizeClass: 'defaultSize',
			tick: 0,
			refresherId: 0,
			weatherStatus: 0
    }
	},
	methods: {
		makeMeBigger: function(e) {
			this.sizeClass = 'getBigger'
		},
		makeDefault: function(e) {
			this.sizeClass = 'defaultSize'
		}
		,
		fetchData: async function() {
			const response = await fetch('https://api.openweathermap.org/data/2.5/weather?zip=' + this.zip + ',us&APPID=37f76ff6a894ea771cfc426192b873cf')
			const json = await response.json()
			console.log(json)
			this.weatherStatus = k2f(json.main.temp)
		}
	},
	mounted: function() {
		this.refresherId = setInterval(() => {
			this.fetchData()
			this.tick++
		}, 5000)
	},
	destroyed: function() {
		clearInterval(this.refresherId)
	}
}
</script>

<style lang="css">
  #borkedApp {
		font-family: Arial, Helvetica, sans-serif;
    color: white;
		border: 3px solid #56b983;
		border-radius: 10px;
		margin: 0 1.5em 0 1.5em;
		background-color: #264456;
		transition: background-color 1s ease-out;
  }
	#borkedApp:hover {
		background-color: #417799;
  	cursor: pointer;
	}
	.defaultSize {
		flex-grow: 1;
	}
	.getBigger {
		flex-grow: 2;
	}
	.removeComponentButton {
		height: 100%;
		width: 100%;
		border: 0;
		border-radius: 5px;
		background-color: #e24466;
		color: #fff;
		font-size: 30px;
	}
	.buttonContainer {
		flex: 0 50px;
	}
</style>