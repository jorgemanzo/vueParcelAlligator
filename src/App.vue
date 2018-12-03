
<template>
  <div id="app">
		<input v-model="newMessage" placeholder="Add a Zipcode">
		<div id="appContainer" class="container">
			<div id="addChild" class="buttonContainer">
				<button v-on:click="makeNewComponent" class="addNewComponent">+</button>
			</div>
			<div class="appsContainer">
				<borked-app
					v-for="child in children"
					v-bind:key="child.id"
					v-bind:zip="child.givenMsg"
					v-on:remove-me="deleteChild(child.id)"
				></borked-app>
			</div>
		</div>

  </div>
</template>

<script>
import borkedApp from './borkedApp.vue'
export default {
  name: 'app',
	components: {
		borkedApp
	},
  data () {
    return {
			children: [
				{ id:1, givenMsg: "97361"},
				{ id:2, givenMsg: "97361"},
				{ id:3, givenMsg: "97361"}
			],
			newMessage: ''
    }
  },
  methods: {
		getMaxId: function(children) {
			let max = 0
			for(let i = 0; i < children.length; i++){
				if(max < children[i].id){
					max = children[i].id
				}
			}
			return max
		},
		makeNewComponent: function() {
			let newId = this.getMaxId(this.children) + 1
			this.children.push({ 'id': newId, 'givenMsg': this.newMessage})
		},
		deleteChild: function(id) {
			for(let i = 0; i < this.children.length; i++){
				if(this.children[i].id == id){
					this.children.splice(i, 1)
					break
				}
			}
		}
  }
}
</script>

<style lang="css">
  .container {
		margin: 10px;
		padding: 10px;
		border: 2px solid black;
		border-radius: 10px;
		min-height: 100px;
		display: flex;
		flex-wrap: wrap;
	}
	.buttonContainer {
		flex: 0 50px;
	}
	.addNewComponent{
		height: 100%;
		width: 100%;
		border: 0;
		border-radius: 5px;
		background-color: #458ce4;
		color: #fff;
		font-size: 30px;
	}
	.appsContainer{
		display: flex;
		flex-direction: row;
		flex-wrap: wrap;
		justify-content: space-evenly;
		border-radius: 5px;
		margin-left: 10px;
	}
</style>