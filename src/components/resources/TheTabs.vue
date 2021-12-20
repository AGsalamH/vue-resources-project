<template>
	<base-card>
		<base-button @click="setSelectedTab('resource-list')" :mode="resourceListSelected">Stored Resources</base-button>
		<base-button @click="setSelectedTab('resource-form')" :mode="resourceFormSelected">Add Resource</base-button>
	</base-card>
	<component :is="selectedTab" @resource-added="setSelectedTab('resource-list')"></component>
</template>

<script>
import ResourceList from './ResourceList.vue';
import ResourceForm from './ResourceForm.vue';

export default {
	data() {
		return {
			selectedTab: 'resource-list',
		};
	},

	methods: {
		setSelectedTab(componentName) {
			this.selectedTab = componentName;
		},
	},

	components: {
		ResourceList,
		ResourceForm,
	},

    computed: {
        resourceListSelected() {
            return this.selectedTab === 'resource-list' ? '' : 'flat';
        },
        resourceFormSelected() {
            return this.selectedTab === 'resource-form' ? '' : 'flat';
        }
    }

};
</script>
