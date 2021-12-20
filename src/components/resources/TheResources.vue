<template>
	<the-tabs></the-tabs>
</template>

<script>
import TheTabs from './TheTabs.vue';
export default {
	data() {
		return {
			resources: [
				{
					id: 'google',
					title: 'Google',
					description: 'Google Search',
					link: 'https://google.com',
				},
				{
					id: 'vuejs',
					title: 'Vue.js',
					description: 'Vue.js official docs',
					link: 'https://vuejs.org',
				},
			],
		};
	},

	methods: {
		addResource(title, description, link) {
			const resource = {
				id: new Date().toISOString(),
				title,
				description,
				link,
			};
			this.resources.push(resource);			
		},

		removeResource(id) {
			const index = this.resources.findIndex(r => r.id === id);
			this.resources.splice(index, 1);
		}


	},

	components: {
		TheTabs,
	},

	provide() {
		return {
			resources: this.resources,
			addResource: this.addResource,
			deleteResource:this.removeResource,
		}
	},

};
</script>

<style scoped></style>
