<template>
	<div id="generator">
		<b-container fluid class="pt-3">
			<b-row>
				<b-col>
					<b-card>
						<b-input-group>
							<b-form-input
								v-model="password"
								type="text"
								placeholder="Your secure password"
								size="lg"
							></b-form-input>
							<b-input-group-append>
								<b-button
									variant="outline-success"
									v-b-tooltip.hover
									title="Copy"
									@click="copyPasswd"
									><b-icon icon="files"></b-icon
								></b-button>
								<b-button
									variant="outline-danger"
									v-b-tooltip.hover
									title="Generate"
									@click="generatePasswd"
									><b-icon icon="arrow-repeat"></b-icon
								></b-button>
							</b-input-group-append>
						</b-input-group>
						<password
							v-model="password"
							:strength-meter-only="true"
							@feedback="showFeedback"
							:secureLength="secLength"
						/>

						<b-card no-body
							><b-list-group flush>
								<b-list-group-item
									v-for="suggestion in suggestions"
									:key="suggestion"
									href="#"
									><b-icon icon="info-circle"></b-icon>
									{{ suggestion }}</b-list-group-item
								>
								<b-list-group-item v-if="warning" href="#"
									><b-icon
										icon="exclamation-triangle"
									></b-icon>
									{{ warning }}</b-list-group-item
								>
							</b-list-group></b-card
						>
					</b-card>
				</b-col>
			</b-row>
		</b-container>

		<b-container fluid class="pt-3">
			<b-row>
				<b-col>
					<b-card header="Customize your password">
						<b-container fluid>
							<b-row align-v="center">
								<b-col>
									<label for="sb-length"
										>Password length</label
									>
									<b-form-spinbutton
										id="sb-length"
										min="8"
										max="128"
										size="lg"
										v-model="length"
									></b-form-spinbutton>
								</b-col>
								<b-col
									class="pt-3 d-flex justify-content-center"
								>
									<b-form-group
										id="cb-strength"
										label="Password options"
									>
										<b-form-checkbox-group
											size="lg"
											switches
											:options="options"
											v-model="checked"
										>
										</b-form-checkbox-group>
									</b-form-group>
								</b-col>
							</b-row>
						</b-container>
					</b-card>
				</b-col>
			</b-row>
		</b-container>
	</div>
</template>

<script>
	import Password from "vue-password-strength-meter";
	import generator from "generate-password";

	export default {
		name: "Generator",
		components: {
			Password,
		},
		data() {
			return {
				password: null,
				suggestions: null,
				warning: null,
				length: 16,
				secLength: 16,
				checked: ["lowercase"],
				options: [
					{ text: "Uppercase", value: "uppercase" },
					{ text: "Lowercase", value: "lowercase" },
					{
						text: "Numbers",
						value: "numbers",
					},
					{ text: "Symbols", value: "symbols" },
					{ text: "Readable", value: "readable" },
				],
			};
		},
		methods: {
			showFeedback({ suggestions, warning }) {
				this.suggestions = suggestions;
				this.warning = warning;
			},
			generatePasswd() {
				if (!this.checked.length) this.checked.push("lowercase");
				this.password = generator.generate({
					length: this.length,
					uppercase: this.checked.includes("uppercase"),
					lowercase: this.checked.includes("lowercase"),
					numbers: this.checked.includes("numbers"),
					symbols: this.checked.includes("symbols"),
					excludeSimilarCharacters: this.checked.includes("readable"),
					strict: true,
				});
			},
			copyPasswd() {
				navigator.clipboard.writeText(this.password);
				this.$bvToast.toast("Password copied to clipboard!", {
					title: "Notification",
					solid: true,
					variant: "success",
					toaster: 'b-toaster-bottom-center'
				});
			},
		},
	};
</script>
