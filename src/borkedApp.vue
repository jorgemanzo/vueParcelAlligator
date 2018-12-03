
import { setInterval } from 'timers';
import { setInterval } from 'timers';
<template>
  <div id="borkedApp" :class="fadeClass">
    <h1>ZIP: {{ zip }}</h1>
		<h3>Weather status: {{ weatherStatus }} F</h3>
		<div v-on:click="$emit('remove-me')" class="buttonContainer">
			<button class="removeComponentButton">X</button>
		</div>
  </div>
</template>

<script>
import k2f from 'kelvin-to-fahrenheit'
import { setTimeout } from 'timers';
export default {
	name: 'borkedApp',
	props: ['zip'],
  data () {
    return {
			fadeClass: 'static',
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
			this.fadeClass = 'fade'
			setTimeout(() => {
				this.fadeClass = 'static'
			}, 1000)
		}
	},
	mounted: function() {
		this.refresherId = setInterval(() => {
			this.fetchData()
		}, 5000)
	},
	destroyed: function() {
		clearInterval(this.refresherId)
	}
}
</script>

<style lang="css">
  #borkedApp {
		font-family: Helvetica, sans-serif;
		display: inline-block;
		padding: 2px 4px;
		border: 4px solid black;
		border-radius: 3px;
		margin: 4px;
		color: black;
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
	.static {
		background-color: white;
	}
	.fade {
		background-color: #c8f9ff;
	}
</style>