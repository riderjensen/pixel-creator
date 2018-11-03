<template>
  <div>
	<div class="input-group mb-3">
		<input type="text" class="form-control" placeholder="CSS Color, Hex, or RBG" v-model="ourColor" v-on:keyup="$emit('color', ourColor)">
	</div>
  </div>
</template>

<script>
export default {
	name: 'Sidebar',
		data: () => {
			return {
				ourColor: ''
			}
		}
	}
</script>

<style scoped>
div{
	height: 100vh;
	background-color: #eee;
}
</style>
