<template>
	<base-dialog v-if="invalidInput" title="Invalid Input" @close="closeDialog">
		<template #default>
			<p>Unfortunately, at least one input value is invalid.</p>
			<p>
				Chech all inputs and make sure you enter at least a few characters..
			</p>
		</template>
		<template #actions>
			<base-button @click="closeDialog">Okay</base-button>
		</template>
	</base-dialog>
	<base-card>
		<form @submit.prevent="handleSubmit">
			<div class="form-control">
				<label for="title">Title</label>
				<input type="text" name="title" id="title" ref="titleInput" />
			</div>
			<div class="form-control">
				<label for="description">Description</label>
				<textarea
					name="description"
					id="description"
					rows="3"
					ref="descriptionInput"
				></textarea>
			</div>
			<div class="form-control">
				<label for="link">Link</label>
				<input type="url" name="link" id="link" ref="linkInput" />
			</div>
			<base-button type="submit">Add Resource</base-button>
		</form>
	</base-card>
</template>

<script>
export default {
	inject: ['addResource'],
	emits: ['resource-added'],
	data() {
		return {
			invalidInput: false,
		};
	},
	methods: {
		handleSubmit() {
			const title = this.$refs.titleInput.value;
			const description = this.$refs.descriptionInput.value;
			const link = this.$refs.linkInput.value;

			// Handle possible errors ...
			if (
				title.trim() === '' ||
				description.trim() === '' ||
				link.trim() === ''
			) {
				this.invalidInput = true;
				return;
			}
			//Add Resource
			this.addResource(title, description, link);

			// Switch to resources tab
			this.$emit('resource-added');
		},

		closeDialog() {
			this.invalidInput = false;
		},
	},
};
</script>

<style scoped>
label {
	font-weight: bold;
	display: block;
	margin-bottom: 0.5rem;
}

input,
textarea {
	display: block;
	width: 100%;
	font: inherit;
	padding: 0.15rem;
	border: 1px solid #ccc;
}

input:focus,
textarea:focus {
	outline: none;
	border-color: #3a0061;
	background-color: #f7ebff;
}

.form-control {
	margin: 1rem 0;
}
</style>
