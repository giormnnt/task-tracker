<template>
	<div :key="task.id" v-for="task in tasks">
		<MyTask :task="task" />
	</div>
</template>

<script>
import MyTask from './MyTask.vue';

export default {
	name: 'MyTasks',
	props: {
		tasks: Array,
	},
	components: {
		MyTask,
	},
};
</script>
