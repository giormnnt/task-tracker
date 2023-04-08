<template>
	<div class="container">
		<MyHeader title="Task Tracker" />
		<MyAddTask @add-task="addTask" />
		<MyTasks
			@toggle-reminder="toggleReminder"
			@delete-task="deleteTask"
			:tasks="tasks"
		/>
	</div>
</template>

<script>
import MyHeader from './components/MyHeader.vue';
import MyTasks from './components/MyTasks.vue';
import MyAddTask from './components/MyAddTask.vue';

export default {
	name: 'App',
	components: {
		MyHeader,
		MyTasks,
		MyAddTask,
	},

	data() {
		return {
			tasks: [],
		};
	},

	methods: {
		addTask(task) {
			this.tasks = [...this.tasks, task];
		},

		deleteTask(id) {
			if (confirm('Are you sure?')) {
				this.tasks = this.tasks.filter(task => task.id !== id);
			}
		},

		toggleReminder(id) {
			this.tasks = this.tasks.map(task =>
				task.id === id ? { ...task, reminder: !task.reminder } : task
			);
		},
	},

	// loads some data when your page/components loads in onCreated
	created() {
		this.tasks = [
			{
				id: 1,
				text: "Doctor's Appointment",
				day: 'April 10th at 4:30pm',
				reminder: true,
			},
			{
				id: 2,
				text: "Michael's Birthday",
				day: 'April 16th at 10:00am',
				reminder: true,
			},
			{
				id: 3,
				text: 'Workout Day',
				day: 'April 18th, at 7:00pm',
				reminder: false,
			},
		];
	},
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');
* {
	box-sizing: border-box;
	margin: 0;
	padding: 0;
}
body {
	font-family: 'Poppins', sans-serif;
}
.container {
	max-width: 500px;
	margin: 30px auto;
	overflow: auto;
	min-height: 300px;
	border: 1px solid steelblue;
	padding: 30px;
	border-radius: 5px;
}
.btn {
	display: inline-block;
	background: #000;
	color: #fff;
	border: none;
	padding: 10px 20px;
	margin: 5px;
	border-radius: 5px;
	cursor: pointer;
	text-decoration: none;
	font-size: 15px;
	font-family: inherit;
}
.btn:focus {
	outline: none;
}
.btn:active {
	transform: scale(0.98);
}
.btn-block {
	display: block;
	width: 100%;
}
</style>
