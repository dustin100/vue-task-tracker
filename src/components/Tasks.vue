<template>
	<div :key="task.id" v-for="task in tasks">
		<Task
			@delete-task="$emit('delete-task', task.id)"
			@set-reminder="$emit('set-reminder', task.id)"
			:task="task"
		/>
	</div>
</template>

<script>
import Task from './Task.vue';
export default {
	name: 'Tasks',
	props: {
		tasks: Array,
	},
	components: {
		Task,
	},
	emits: ['deletes-task', 'set-reminder'],
};
</script>
