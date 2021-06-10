<template>
	<v-container fluid fill-height>
		<v-row justify="center">
			<div>
				<p class="text-md-body1 text-center">
					This URL shortening app was designed by Boye Adeotan using the Bit.ly
					api and Vuetify .
				</p>
				<router-link to="/" class="mr-2 color: putple--text"
					>Back to home</router-link
				>
			</div>
		</v-row>

		<v-row justify="center">
			<div>
				<v-btn class="ma-2" href="https://github.com/Rippyblogger"
				target="_blank">
					Visit my Github Page
					<v-icon class="pl-2">mdi-github</v-icon>
				</v-btn>

				<v-btn class="ma-2" href="https://linkedin.com/in/adeboye-adeotan"
				target="_blank">
					Visit my LinkedIn Page
					<v-icon class="pl-2">mdi-LinkedIn</v-icon>
				</v-btn>
			</div>
		</v-row>
	</v-container>
</template>

<script>
export default {
	name: "About",
};
</script>

<style scoped>
a {
	text-decoration: none;
}

a:hover{
  text-decoration: underline;
}

</style>
