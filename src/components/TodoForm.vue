<template>
	<form @submit.prevent="saveTodo">
		<h1>Редактирование заметки</h1>
		<div class="form-group">
			<input name="title" type="text" class="form-control" v-model="todo['title']"/>
		</div>
		<div class="form-group">
			<textarea rows="10" name="text" class="form-control" v-model="todo['text']"></textarea>
		</div>
		<div class="d-flex justify-content-between">
			<button @click="cancelTodo" class="btn btn-secondary">Закрыть</button>
			<button type="submit" class="btn btn-primary">Сохранить</button>
		</div>
	</form>
</template>

<script>
export default {
	props: ['todo'],
	methods: {
		saveTodo() {
			this.$emit('save-todo', JSON.stringify(this.todo), this.todo["id"]);
		},
		cancelTodo() {
			this.$emit('cancel-todo')
		}
	}
}
</script>