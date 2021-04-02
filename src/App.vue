<template>
	<div id="app" class="container">
		<div class="main-page" v-if="page === 'list'">
			<TodoList v-bind:todos="limitTodos.length > 0 ? limitTodos : todos.slice(this.maxItemsOnPage * this.nowPage - this.maxItemsOnPage, this.maxItemsOnPage * this.nowPage)" 
						@edit-todo="editTodo"/>
			<Pagination v-bind:count="localTodos.length > 0 ? localTodos.length : todos.length"
						v-bind:maxElem="maxItemsOnPage"
						v-bind:page="nowPage"
						@change-page="changePage"/>
		</div>
		<TodoForm v-bind:todo="todoData" 
					@save-todo="saveTodo" 
					@cancel-todo="cancelTodo" 
					v-else/>

	</div>
</template>

<script>
import TodoList from '@/components/TodoList';
import TodoForm from '@/components/TodoForm';
import Pagination from '@/components/Pagination';
export default {
	name: "App",
	components: {
		TodoList, TodoForm, Pagination
	},
	data() {
		return {
			todos: [{"id": 1,"title": "Заметка 1", "date": "01/01/2000", "text": "Текст заметки 1"},
						{"id": 2,"title": "Заметка 2", "date": "02/01/2000", "text": "Текст заметки 2"},
						{"id": 3,"title": "Заметка 3", "date": "03/01/2000", "text": "Текст заметки 3"},
						{"id": 4,"title": "Заметка 4", "date": "04/01/2000", "text": "Текст заметки 4"},
						{"id": 5,"title": "Заметка 5", "date": "05/01/2000", "text": "Текст заметки 5"},
						{"id": 6,"title": "Заметка 6", "date": "06/01/2000", "text": "Текст заметки 6"},
						{"id": 7,"title": "Заметка 7", "date": "07/01/2000", "text": "Текст заметки 7"},
						{"id": 8,"title": "Заметка 8", "date": "08/01/2000", "text": "Текст заметки 8"},
						{"id": 9,"title": "Заметка 9", "date": "09/01/2000", "text": "Текст заметки 9"},],
			page: 'list',
			todoData: {},
			maxItemsOnPage: 3,
			nowPage: 1
		}
	},
	computed: {
		localTodos() {
			const todos = [];
				for (let i = 0; i < localStorage.length; i++) {
					if (localStorage[localStorage.key(i)].match(/{"id"/)) {
						todos.push(JSON.parse(localStorage[localStorage.key(i)]));
					}
				}

			return todos.sort((a, b) => +a["id"] - +b["id"]);
		},
		limitTodos() {
			return this.localTodos.slice(this.maxItemsOnPage * this.nowPage - this.maxItemsOnPage, this.maxItemsOnPage * this.nowPage);
		}
	},
	mounted() {
		this.todos.forEach(todo => {
			if (!localStorage.getItem(todo['id'])) {
				localStorage.setItem(todo['id'], JSON.stringify(todo));
			}
		})
	},
	methods: {
		editTodo(todo) {
			this.page = 'form';
			this.todoData = todo;
		},
		saveTodo(todo, id) {
			this.page = 'list';
			this.todoData[id - 1] = todo;
			localStorage.setItem(id, todo);
		},
		cancelTodo() {
			this.page = 'list';
		},
		changePage(page) {
			this.nowPage = page;
		}
	}
};
</script>

<style>
	* {
		padding: 0;
		margin: 0;
	}
	#app {
		font-family: Avenir, Helvetica, Arial, sans-serif;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
		text-align: center;
		color: #2c3e50;
		margin-top: 60px;
	}
</style>
