<template>
	<v-flex sm8 offset-sm2>
		<v-card>
			<v-toolbar dark>
				<v-toolbar-title
					>New Message
					<span
						v-if="success != null"
						class="badge badge-pill text-dark bg-light p-2"
						>{{ success }}</span
					></v-toolbar-title
				>
			</v-toolbar>
			<v-form>
				<v-container>
					<v-layout>
						<v-flex xs12 md4>
							<v-text-field
								label="Message"
								required
								v-model="messageBody"
							></v-text-field>
						</v-flex>
					</v-layout>
				</v-container>
				<v-btn @click="submit">submit</v-btn>
			</v-form>
		</v-card>
	</v-flex>
</template>

<script>
//import axios from "axios";
//import store from "../store.js";

export default {
	data() {
		return {
			messages: [],
			messageBody: null,
			error: null,
			success: null,
		};
	},
	methods: {
		async submit() {
			try {
				this.$store.dispatch("newMessage", this.messageBody).then(
					(data) => {
						console.log(data);
						this.success = data.message;
					},
					(error) => {
						this.error = error;
					}
				);
			} catch (error) {
				this.error = error;
			}
		},
	},
};
</script>
