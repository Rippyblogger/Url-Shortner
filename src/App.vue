<template>
	<v-app>
		<v-app-bar app color="purple" dark>
			<div class="d-flex align-center">
				<v-img
					alt="Url Logo"
					class="shrink mr-2"
					contain
					src="../src/assets/url-icon.png"
					transition="scale-transition"
					width="40"
				/>
			</div>

			<div text-h5 class="font-weight-medium">
				<router-link class="color: white--text" to="/">SHORTEN ME</router-link>
			</div>

			<v-spacer></v-spacer>

			<v-btn href="../src/views/About.vue" text>
				<router-link to="/about" class="mr-2 color: white--text">About</router-link>
				<v-icon>mdi-open-in-new</v-icon>
			</v-btn>
		</v-app-bar>

		<v-main>
			<router-view />
		</v-main>
	</v-app>
</template>

<script>
export default {
	name: "App",

	data: () => ({
		//
	}),
};
</script>

<style>
div.router-link {
	text-decoration: none;
}

a {
	text-decoration: none;
}
</style>
