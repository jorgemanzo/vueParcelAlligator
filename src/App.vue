
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
				v-bind:msg="child.givenMsg"
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
				{ id:1, givenMsg: "SCREAMING!!"},
				{ id:2, givenMsg: "SCREAMING!!"},
				{ id:3, givenMsg: "SCREAMING!!"}
			],
			newMessage: ''
    }
  },
  methods: {
		makeNewComponent: function() {
			this.children.push({ 'id': this.children.length + 1, 'givenMsg': this.newMessage})
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