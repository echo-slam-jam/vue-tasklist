<template>
	<div id="task-table">
		<p v-if = "tasklist.length < 1" class = "empty-table">Something is wrong :)
		</p>
		<table v-else>
			<thead>
				<tr>
					<th>Task name</th>
					<th>Date Due</th>
					<th>Actions</th>
				</tr>
			</thead>
			<tbody>
				<tr v-for="task in tasklist" :key="task.id">
					<td v-if = "editing === task.id">
						<input type="text" v-model = "task.name">
					</td>
					<td v-else>{{ task.name }}</td>
					<td v-if = "editing === task.id">
						<input type="text" v-model = "task.date">
					</td>
					<td v-else>{{ task.date }}</td>
					<td v-if = "editing === task.id">
						<button @click = "editTask(task)">
							Save
						</button>
						<button class = "muted-button" @click = "cancelEdit(task)"> Cancel</button>
					</td>
					<td v-else>
						<button @click = "editMode(task)">Edit</button>
						<button @click = "$emit('delete:task', task.id)">Delete</button>
					</td>
				</tr>	
			</tbody>
		</table>
	</div>
</template>

<script>
	export default {
		name: 'task-table',
		props: {
  tasklist: Array,
    },
    data() {
		return {
			editing: null,
		}
    },
    methods: {
		editMode(task) {
			this.cachedTask = Object.assign({}, task)
			this.editing = task.id
		},
		editTask(task) {
			if (task.name === '' || task.date === '') return
				this.$emit('edit:task', task.id, task)
				this.editing = null
		},
		cancelEdit(task) {
			Object.assign(task, this.cachedTask)
			this.editing = null;
		}
    }
}
</script>

<style scoped>
	button {
    margin: 0 0.5rem 0 0;
  }
</style>