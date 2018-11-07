<template>
  <div id="app">
	<link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.1.3/css/bootstrap.min.css" integrity="sha384-MCw98/SFnGE8fJT3GXwEOngsV7Zt27NXFoaoApmYm81iuXoPkFOJwJ8ERdknLPMO" crossorigin="anonymous">
	<div class="container-fluid">
	<div class="row">
		<div class="col-sm-10">
			<div class="row">
				<div class="col-sm-12">
					<div v-for="index in 10" :key="index">
						<div class="row">
							<div v-for="index in 10" :key="index">
								<PixelBlock v-bind:color="currentColor"  />
							</div>
						</div>	
					</div>
				</div>
			</div>
		</div>
		<div class="col-sm-2">
			<div class="row">
				<div class="col-sm-12">
					<Sidebar v-on:color="addColor" />
				</div>
			</div>
		</div>
	</div>
	</div>
  </div>
</template>

<script>
import PixelBlock from './components/PixelBlock.vue'
import Sidebar from './components/Sidebar.vue'

export default {
  name: 'app',
  components: {
	PixelBlock,
	Sidebar
  },
    data: () => {
    return {
		squareGrid: 10,
		currentColor: ''
    };
  },
  methods: {
		addColor: function(color){
			this.currentColor = color;
		}
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  overflow:hidden;
}
</style>
