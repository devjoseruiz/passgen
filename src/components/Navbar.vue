<template>
	<div id="navbar">
		<b-navbar fixed="top" toggleable="lg" type="dark" variant="danger">
			<b-navbar-brand
				><b-icon icon="shield-lock-fill"></b-icon>
				PassGen</b-navbar-brand
			>

			<b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

			<b-collapse id="nav-collapse" is-nav>
				<b-navbar-nav class="ml-auto">
					<b-nav-item
						href="https://gitlab.com/joseruizdev/passgen"
						target="_blank"
					>
						<b-button variant="outline-light">
							<b-icon icon="code-square"></b-icon> Fork me!
						</b-button>
					</b-nav-item>
				</b-navbar-nav>
			</b-collapse>
		</b-navbar>
	</div>
</template>

<script>
	export default {
		name: "Generator",
	}
</script>
