<template>
	<div>
		<h1>Заметки</h1>
		<ul>
			<TodoItem 
				v-for="(todo, i) of todos"
				:key="todo.id"
				v-bind:todo="todo"
				v-bind:index="i"
				@edit-todo="editTodo"/>
		</ul>
	</div>
</template>

<script>
import TodoItem from '@/components/TodoItem';
export default({
	props: ['todos'],
	components: {
		TodoItem
	},
	methods: {
		editTodo(elem) {
			this.$emit('edit-todo', elem);
		}
	}
})
</script>

<style scoped>

</style>