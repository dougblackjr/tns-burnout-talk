<template>
	<div class="container m-auto">
		<h1 class="font-bold text-3xl text-center text-indigo-700 my-4">I'm Not Growing Up, I'm Just Burning Out</h1>
		<h2 class="font-bold text-xl text-center text-indigo-700 mb-4">EE Conf Talk - 2022</h2>
		<p class="font-bold text-md text-center text-gray-700 mb-4">Here is a list of a few resources for the talk, and from the talk. We track no data on this site, and no tracking cookies are installed.</p>
		<ul class="flex flex-col md:flex-row justify-around">
			<li>
				<a href="#" v-on:click.prevent="componentName = 'quizlet'" class="cursor-pointer">Take Assessment</a>
			</li>
			<li>
				<a href="#" v-on:click.prevent="componentName = 'resources'" class="cursor-pointer">Resources</a>
			</li>
			<li>
				<a href="https://eeconf.com/" target="_blank" class="cursor-pointer">EEConf</a>
			</li>
			<li>
				<a href="https://docs.google.com/presentation/d/1V7l920bUxe0-cf1WOLKy6kG70Rp74MmQeFMvSVIE31Y/edit?usp=sharing" target="_blank" class="cursor-pointer">Slides</a>
			</li>
			<li>
				<a href="https://triplenerdscore.net" target="_blank" class="cursor-pointer">TNS</a>
			</li>
		</ul>
		<component
			v-if="componentName"
			:is="componentName"
			v-on:change-page="changePage"
		></component>
	</div>
</template>

<script>
	import Quizlet from './pages/Quizlet.vue'
	import Resources from './pages/Resources.vue'
	export default {
		name: 'HelloWorld',
		components: {
			Quizlet,
			Resources
		},
		data() {
			return {
				componentName: 'quizlet'
			}
		},
		props: {
			msg: String
		},
		methods: {
			changePage(name) {
				this.componentName = name
			}
		}
	}
</script>