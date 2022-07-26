<template>
	<AddTask v-show="showAddTask" @add-task="addTask" />
	<Tasks @delete-task="deleteTask" @set-reminder="setReminder" :tasks="tasks" />
</template>

<script>
import Header from '../components/Header.vue';
import Tasks from '../components/Tasks.vue';
import AddTask from '../components/AddTask.vue';

export default {
	name: 'Home',
	props: {
		showAddTask: Boolean,
	},
	components: {
		Header,
		Tasks,
		AddTask,
	},
	data() {
		return {
			tasks: [],
		};
	},
	methods: {
		async setReminder(id) {
			const taskToToggle = await this.fetchTask(id);
			const updateTask = { ...taskToToggle, reminder: !taskToToggle.reminder };

			const res = await fetch(`api/tasks/${id}`, {
				method: 'PUT',
				headers: { 'Content-type': 'application/json' },
				body: JSON.stringify(updateTask),
			});

			const data = await res.json();
			this.tasks = this.tasks.map((task) => {
				return task.id === id ? { ...task, reminder: data.reminder } : task;
			});
		},
		async addTask(task) {
			const res = await fetch('api/tasks', {
				method: 'Post',
				headers: { 'Content-type': 'application/json' },
				body: JSON.stringify(task),
			});

			const data = await res.json();
			this.tasks = [...this.tasks, data];
		},

		async deleteTask(id) {
			const res = await fetch(`api/tasks/${id}`, {
				method: 'Delete',
			});
			res.status === 200
				? (this.tasks = this.tasks.filter((task) => {
						return task.id !== id;
				  }))
				: alert('error deleting task');
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
	async created() {
		this.tasks = await this.fetchTasks();
	},
};
</script>

<style></style>
