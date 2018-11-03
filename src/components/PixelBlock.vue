<template>
  <div>
    {{ newColor }}
  </div>
</template>

<script>
export default {
	name: 'PixelBlock',
	props: ['color'],
	data: function () {
		return {
			newColor: this.color
		}
	}
}
</script>


<style scoped>
div{
	height: 10vh;
	width: 10vh;
	background-color: #fff;
	
}
div:hover{
	box-shadow: 1px 1px 3px;
	transform: translateY(-1px);
	transform: translateX(1px);
}
</style>
