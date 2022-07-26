<template>
	<header>
		<h1>{{ title }}</h1>
		<Button
			v-show="homePage"
			@btn-click="$.emit('toggle-add-task')"
			:text="open ? 'Close' : 'Add Task'"
			:color="open ? 'Red' : 'Green'"
		/>
	</header>
</template>

<script>
import Button from './Button.vue';
export default {
	name: 'Header',
	props: {
		title: String,
		open: Boolean,
	},
	components: {
		Button,
	},
	computed: {
		homePage() {
			if (this.$route.path === '/') {
				return true;
			} else {
				return false;
			}
		},
	},
};
</script>

<style scoped>
header {
	display: flex;
	justify-content: space-between;
	align-items: center;
	margin-bottom: 20px;
}
</style>
