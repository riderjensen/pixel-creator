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
import CommonColor from './CommonColor.vue'

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
			const {body} = document

			const canvas = document.createElement('canvas')
			const ctx = canvas.getContext('2d')
			canvas.width = canvas.height = 100

			const tempImg = document.createElement('img')
			tempImg.addEventListener('load', onTempImageLoad)
			let ourTest = document.getElementById("myTestHere").outerHTML;
			tempImg.src = 'data:image/svg+xml,' + encodeURIComponent('<svg xmlns="http://www.w3.org/2000/svg" width="100" height="100"><foreignObject width="100%" height="100%"><div xmlns="http://www.w3.org/1999/xhtml">'+ourTest+'</div></foreignObject></svg>')

			const targetImg = document.createElement('img')
			body.appendChild(targetImg)

			function onTempImageLoad(e){
			ctx.drawImage(e.target, 0, 0)
			targetImg.src = canvas.toDataURL()
			}
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
