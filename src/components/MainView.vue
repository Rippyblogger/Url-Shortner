<template>
	<v-container fluid fill-height>
		<v-row align-content="center" justify="center">
			<v-col xs="2" sm="3" md="2">
				<v-select
					class="text-center"
					:items="protocol"
					label="Select Protocol"
					:menu-props="{ top: true, offsetY: true }"
					solo
					v-model="protocolChoice"
				>
				</v-select>
			</v-col>

			<v-col cols="6">
				<v-text-field
					label="URL"
					outlined
					clearable
					v-model="enteredUrl"
					append-icon="mdi-link"
					:rules="[rules.required]"
					hint="Select either http:// or https:// from the dropdown and enter url"
				>
				</v-text-field>

				<p v-if="showError" class="color: red--text  text-center">
					<span><v-icon>error</v-icon></span> {{ errorMessage }}
				</p>

				<v-btn @click="shortenThis(enteredUrl)"  v-bind="size" color="purple"
					>SHORTEN LINK</v-btn
				>

				<v-text-field
					v-if="showShortened"
					id="copyText"
					filled
					class="mt-5"
					label="URL"
					outlined
					readonly
					v-model="shortenedLink"
					append-icon="mdi-content-copy"
					@click:append="copyThis"
					hint="Click the icon to copy"
				>
				</v-text-field>

				<p v-if="confirmCopy" class="color: purple--text  text-center">
					<span><v-icon>mdi-DoneOutline</v-icon></span> {{ successMessage }}
				</p>
			</v-col>
		</v-row>
	</v-container>
</template>

<script>
export default {
	name: "MainView",
	data() {
		return {
			enteredUrl: "",
			shortenedLink: "",
			token: "643a63095646f5687867801ec981e5b36fba721d",
			endpoint: "https://api-ssl.bitly.com/v4/shorten",
			headers: {
				Authorization: "643a63095646f5687867801ec981e5b36fba721d",
				"Content-Type": "application/json",
			},
			errorMessage: "",
			showError: false,
			protocol: ["HTTPS://", "HTTP://"],
			protocolChoice: "",
			rules: {
				required: (value) => !!value || "Required.",
			},
			showShortened: false,
			confirmCopy: false,
		};
	},
	methods: {
		shortenThis: async function(longurl) {
			if (longurl.includes("www") || this.protocolChoice == false) {
				this.showError = !this.showError;
				this.errorMessage =
					"Please exclude the www prefix or select a protocol";
			} else if (longurl && this.protocolChoice) {
				let conjoined = `${this.protocolChoice}${longurl}`;
				await fetch("https://api-ssl.bitly.com/v4/shorten", {
					method: "POST",
					mode: "cors",
					headers: this.headers,
					body: JSON.stringify({ long_url: conjoined, domain: "bit.ly" }),
				})
					.then((response) => response.json())
					.then((data) => (this.shortenedLink = data.link))
					.catch((error) => console.log(error))
					.finally(() => (this.showShortened = !this.showShortened));
			} else {
				this.showError = !this.showError;
				this.errorMessage = "Please enter a valid url";
			}
		},

		copyThis: function() {
			let textToCopy = document.querySelector("#copyText");
			textToCopy.setAttribute("type", "text"); //
			textToCopy.select();

			try {
				var successful = document.execCommand("copy");
				var msg = successful ? "successful" : "unsuccessful";
				this.confirmCopy = !this.confirmCopy;
				this.successMessage = `Shortened Url copy ${msg}`;
			} catch (err) {
				alert("Unable to copy");
			}
		},
	},
	computed: {
		size() {
			const size = {sm: "small", lg: "large", xl: "x-large" }[
				this.$vuetify.breakpoint.name
			];
			return size ? { [size]: true } : {};
		},
	},
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Nunito:ital,wght@0,200;0,300;0,400;0,700;1,200;1,300&family=Stalemate&display=swap");

.mytext {
	font-family: "Stalemate", cursive;
}
</style>
