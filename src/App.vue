<template>
	<div id="app">
		<Navbar />
		<b-container class="pt-3">
			<h1 class="text-center">
				<strong>Password generator tool</strong>
			</h1>
			<h4 class="text-center text-muted">
				Instantly create a secure, random password
			</h4>
		</b-container>
		<Generator />
	</div>
</template>

<script>
	import Navbar from "@/components/Navbar.vue";
	import Generator from "@/components/Generator.vue";

	export default {
		name: "App",
		components: {
			Navbar,
			Generator,
		},
	};
</script>

<style>
	#app {
		margin-top: 70px;
		margin-bottom: 30px;
	}
</style>
