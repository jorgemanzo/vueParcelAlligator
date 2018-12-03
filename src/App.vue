
<template>
  <div id="app">

		<div id="addChild">
			<input v-model="newMessage" placeholder="Text in new component">
			<button v-on:click="makeNewComponent">Create</button>
		</div>

		<div id="appContainer">
			<borked-app
				v-for="child in children"
				v-bind:key="child.id"
				v-bind:zip="child.givenMsg"
				v-on:remove-me="deleteChild(child.id)"
			></borked-app>
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
  #appContainer {
    border: 3px solid grey;
		border-radius: 10px;
		display: flex;
		flex-direction: row;
		flex-wrap: wrap;
		justify-content: space-evenly;
  }
</style>