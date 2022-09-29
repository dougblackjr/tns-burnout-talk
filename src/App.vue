<template>
	<img src="./assets/tns-logo.png" alt="tripleNERDscore logo" class="logo m-auto">
	<HelloWorld />
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
	name: 'App',
	components: {
		HelloWorld
	},
	mounted() {
		console.log('Hi there! We left a bunch of consoles in the code so you can see how things are figured out. Enjoy!')
	}
}
</script>

<style>
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	text-align: center;
	color: #2c3e50;
	margin-top: 60px;
}
</style>
