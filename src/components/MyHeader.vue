<template>
	<header>
		<h1>{{ title }}</h1>
		<MyButton
			v-if="homePage"
			@btn-click="$emit('toggle-add-task')"
			:text="showAddTask ? 'Close' : 'Add Task'"
			:color="showAddTask ? 'red' : 'green'"
		/>
	</header>
</template>

<script>
import MyButton from './MyButton.vue';

export default {
	name: 'MyHeader',
	props: {
		title: String,
		showAddTask: Boolean,
	},
	components: { MyButton },

	computed: {
		homePage() {
			if (this.$route.path === '/') return true;
			else return false;
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
