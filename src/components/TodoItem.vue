<template>
	<li class="row justify-content-between">
		<div class="li-left d-flex flex-column">
			<h5>{{todo.title}}</h5>
			<span>{{todo.date}}</span>
		</div>
		<button class="btn btn-primary align-self-center"
				@click="editTodo(todo)">Редактировать</button>
	</li>
</template>

<script>
export default {
	props: ['todo', 'index'],
	methods: {
		editTodo(elem) {
			this.$emit('edit-todo', elem)
		}
	}
}
</script>

<style scoped>
	li {
		border-bottom: 1px solid #ccc;
		padding: 1rem 0;
	}
	li:last-child {
		border-bottom: none;
	}
	.li-left {
		text-align: left;
	}
	h5 {
		font-weight: bold;
		font-size: 18px;
	}
	span {
		font-style: italic;
	}
</style>