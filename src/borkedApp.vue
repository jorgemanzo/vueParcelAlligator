
import { setInterval } from 'timers';
import { setInterval } from 'timers';
<template>
  <div id="borkedApp" 
		:class="sizeClass" 
		v-on:mouseover="makeMeBigger" 
		v-on:mouseleave="makeDefault"
		v-on:click="$emit('remove-me')"
		>
    <h1>{{ msg }}</h1>
		<p>{{ tick }}
  </div>
</template>

<script>
export default {
	name: 'borkedApp',
	props: ['msg'],
  data () {
    return {
			sizeClass: 'defaultSize',
			tick: 0		
    }
	},
	methods: {
		makeMeBigger: function(e) {
			this.sizeClass = 'getBigger'
		},
		makeDefault: function(e) {
			this.sizeClass = 'defaultSize'
		},
		getData: async () => {
			const response = await fetch('https://api.openweathermap.org/data/2.5/weather?zip=97361,us&APPID=37f76ff6a894ea771cfc426192b873cf')
			const json = await response.json()
			console.log(data);
		}
	},
	mounted: function() {
		setInterval(() => {
			this.tick++
			this.getData()
		}, 5000)
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
</style>