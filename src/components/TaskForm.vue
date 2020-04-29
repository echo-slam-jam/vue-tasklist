<template>
	<div id="task-form">
		<form @submit.prevent="handleSubmit">
			<label>Task Name</label>
			<input ref = "first"
			v-model="task.name" 
			type="text"
			:class="{ 'has-error': submitting && invalidName }"
			@focus="clearStatus"
			@keypress="clearStatus"
			/>
			<label>Task Date</label>
			<input 
			v-model="task.date" 
			type="text"
			:class="{ 'has-error': submitting && invalidDate }"
			@focus="clearStatus" 
			/>
			<p v-if = "success" class = "success-message">
				Task successfully added
			</p>
			<p v-if = "error && submitting" class = "error-message">
				❗Please fill out all required fields
			</p>
			
			<button>Add Task</button>
		</form>
	</div>
</template>

<script>
	export default {
		name: 'task-form',
		data() {
			return {
submitting: false,
error: false,
success: false,
				task: {
					name: '',
					date: '',
				},
			}
		},
		computed: {
  invalidName() {
    return this.task.name === ''
  },

  invalidDate() {
    return this.task.date === ''
  },
},
		methods: {
			handleSubmit() {
				this.submitting = true
				this.clearStatus()

				if (this.invalidName || this.invalidDate) {
					this.error = true
					return
				}

				this.$emit('add:task', this.task)
				this.$refs.first.focus()
				this.task = {
					name: '',
					date: '',
				}
				this.error = false
				this.success = true
				this.submitting = false
			},
			clearStatus() {
				this.success = false
				this.error = false
			}
		}
	}
</script>

<style scoped>
  form {
    margin-bottom: 2rem;
  }

  [class*='-message'] {
    font-weight: 500;
  }

  .error-message {
    color: #d33c40;
  }

  .success-message {
    color: #32a95d;
  }
</style>