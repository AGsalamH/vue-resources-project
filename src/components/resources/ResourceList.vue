<template>
	<ul>
		<resource-detail v-for="res in resources" :key="res.id" :resource="res">
		</resource-detail>
	</ul>
</template>

<script>
import ResourceDetail from './ResourceDetail.vue';
export default {
	inject: ['resources'],
	components: {
		ResourceDetail,
	},
};
</script>

<style scoped>
ul {
	list-style: none;
	margin: 0;
	padding: 0;
	margin: auto;
	max-width: 40rem;
}
</style>
