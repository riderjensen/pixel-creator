<template>
  <div class="side">
	  <div class="input-group mb-3">
		  <p>Click a button or enter a number</p>
		<button class="btn btn-primary" @click="$emit('pixelNum', 10)">10</button>
		<button class="btn btn-primary" @click="$emit('pixelNum', 20)">20</button>
		<button class="btn btn-primary" @click="$emit('pixelNum', 25)">25</button>
		<button class="btn btn-primary" @click="$emit('pixelNum', 30)">30</button>
		<button class="btn btn-primary" @click="$emit('pixelNum', 40)">40</button>
		<br />

		<input type="num" class="form-control" placeholder="Number" v-model="ourPixelNumbers" v-on:keyup="$emit('pixelNum', ourPixelNumbers)" />
		<br />
	</div>
		<button class="btn btn-primary" @click="exportImg">Export</button>
	<div class="input-group mb-3">
		<input type="text" class="form-control" placeholder="CSS Color, Hex, or RGB" v-model="ourColor" v-on:keyup="$emit('color', ourColor)" />
		<br />
	</div>
	<button class="btn btn-primary" @click="pushColor(ourColor)">Add Color</button>
	<button class="btn btn-danger" @click="deleteColor(ourColor)">Delete Color</button>
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
import CommonColor from './CommonColor.vue';
import html2canvas from 'html2canvas';

export default {
	name: 'Sidebar',
	components: {
		CommonColor
	},
	data: () => {
		return {
			ourColor: '',
			commonColorsArray: ['black','white','gray','red', 'green', 'blue', 'yellow', 'tan', 'rebeccapurple'],
			ourPixelNumbers: 10
		}
	},
	watch: {
		ourColor: function () {
			this.$emit('color', this.ourColor);
		}
	},
	methods: {
		pushColor(color) {
			if(!this.commonColorsArray.includes(color)){
				this.commonColorsArray.push(color);
			}
		},
		deleteColor(color) {
			if(this.commonColorsArray.includes(color)){
				let index = this.commonColorsArray.indexOf(color);
				this.commonColorsArray.splice(index, 1);
			}
		},
		setColor(incColor) {
			this.ourColor = incColor;
		},
		exportImg() {
			// remove styling on each pixel block and 
			html2canvas(document.querySelector("#myTestHere"), {
				canvas: null
			}).then(function(canvas) {
    			document.body.appendChild(canvas);
			})
			
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
.flexRow{
	display: flex;
	flex-wrap: wrap;
}
</style>
