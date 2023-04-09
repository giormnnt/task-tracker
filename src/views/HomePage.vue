<template>
	<MyAddTask v-if="showAddTask" @add-task="addTask" />
	<MyTasks
		@toggle-reminder="toggleReminder"
		@delete-task="deleteTask"
		:tasks="tasks"
	/>
</template>

<script>
import MyTasks from '../components/MyTasks.vue';
import MyAddTask from '../components/MyAddTask.vue';

export default {
	name: 'HomePage',
	props: {
		showAddTask: Boolean,
	},
	components: {
		MyTasks,
		MyAddTask,
	},

	data() {
		return {
			tasks: [],
		};
	},

	methods: {
		async addTask(task) {
			const res = await fetch('api/tasks', {
				method: 'POST',
				headers: {
					'Content-Type': 'application/json',
				},
				body: JSON.stringify(task),
			});

			const data = await res.json();
			this.tasks = [...this.tasks, data];
		},

		async deleteTask(id) {
			if (confirm('Are you sure?')) {
				const res = await fetch(`api/tasks/${id}`, {
					method: 'DELETE',
				});

				res.status === 200
					? (this.tasks = this.tasks.filter(task => task.id !== id))
					: alert('Error deleting task');
			}
		},

		async toggleReminder(id) {
			const taskToToggle = await this.fetchTask(id);
			const updateTask = { ...taskToToggle, reminder: !taskToToggle.reminder };

			const res = await fetch(`api/tasks/${id}`, {
				method: 'PUT',
				headers: {
					'Content-type': 'application/json',
				},
				body: JSON.stringify(updateTask),
			});

			const data = await res.json();

			this.tasks = this.tasks.map(task =>
				task.id === id ? { ...task, reminder: data.reminder } : task
			);
		},

		async fetchTasks() {
			const res = await fetch('api/tasks');
			const data = await res.json();
			return data;
		},

		async fetchTask(id) {
			const res = await fetch(`api/tasks/${id}`);
			const data = await res.json();
			return data;
		},
	},

	// loads some data when your page/components loads in onCreated
	async created() {
		this.tasks = await this.fetchTasks();
	},
};
</script>
