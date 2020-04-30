<template>
	<div id="task-table">
		<p v-if="tasklist.length < 1" class="empty-table">Something is wrong :)
		</p>
		<v-simple-table fixed-header height="300px" v-else>
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
						<v-text-field autofocus type="text" v-model="task.name"/>
					</td>
					<td v-else>{{ task.name }}</td>
					<td v-if = "editing === task.id">
						<v-text-field type="text" v-model="task.date"/>
					</td>
					<td v-else>{{ task.date }}</td>
					<td v-if = "editing === task.id">
						<v-btn @click="editTask(task)">
							Save
						</v-btn>
						<v-btn class = "muted-button" @click="cancelEdit(task)"> Cancel</v-btn>
					</td>
					<td v-else>
						<v-btn color="blue lighten-3" @click="editMode(task)">Edit</v-btn>
						<v-btn color="error" @click="$emit('delete:task', task.id)">Delete</v-btn>
					</td>
				</tr>	
			</tbody>
		</v-simple-table>
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