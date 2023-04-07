<template>
	<header>
		<h1>{{ title }}</h1>
		<MyButton text="Add Task" color="green" />
	</header>
</template>

<script>
import MyButton from './MyButton.vue';

export default {
	name: 'MyHeader',
	props: {
		title: String,
	},
	components: { MyButton },
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
