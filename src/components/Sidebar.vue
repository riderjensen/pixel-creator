<template>
  <div class="side">
	<div class="input-group mb-3">
		<input type="text" class="form-control" placeholder="CSS Color, Hex, or RGB" v-model="ourColor" v-on:keyup="$emit('color', ourColor)" />
		<br />
	</div>
	<button class="btn btn-primary" @click="pushColor(ourColor)">Add Color</button>
	<p>Our Color: <span class="colorShow" :style="{backgroundColor: ourColor}"></span></p>
	<br />
	<p>Common colors used</p>
	<div class="flexRow">
		<div v-for="index in commonColorsArray" :key="index">
			<CommonColor :smallColor="index" v-on:sendsmallcolor="setColor" />
		</div>
	</div>
  </div>
</template>



<script>
import CommonColor from './CommonColor.vue'

export default {
	name: 'Sidebar',
	components: {
		CommonColor
	},
	data: () => {
		return {
			ourColor: '',
			commonColorsArray: ['red', 'green', 'blue', 'yellow']
		}
	},
	methods: {
		pushColor(color) {
			this.commonColorsArray.push(color);
		},
		setColor(incColor){
			this.ourColor = incColor;
		},
		foo(){
			console.log('testing')
		}
	}
}
</script>

<style scoped>
div.side{
	height: 100vh;
	background-color: #eee;
}
span.colorShow{
	display: inline-block;
	height: 15px;
	width: 15px;
}
</style>
