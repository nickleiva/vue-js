<template>
	<div class="issues-app">
		<br />
		<h1>TODO LIST</h1>
		<br />
		<form @submit.prevent="onAddTodo" class="add-issue-form">
			<div class="input-container">
				<el-input
					v-model="todo"
					type="text"
					id="issue"
					placeholder="Enter a new issue"
				/>
				<br /><br />
				<el-button type="success" @click="onAddTodo">Add new</el-button>
			</div>
		</form>

		<el-row :gutter="12" class="issue-list">
			<TodoItem v-for="( todo, index ) in todos" :key="index" :index="index" :todo="todo" @close-todo="completeTodo"/>
		</el-row>

		<el-row :gutter="12" class="issue-list">
			<TodoItem v-for="( issue, index ) in issues" :key="index" :index="index" :todo="issue.title" @close-todo="closeIssue"  />
		</el-row>
	</div>
</template>

<script>
import axios from "axios";
import TodoItem from '@/components/TodoItem.vue';

const client = axios.create({
	baseURL: `${process.env.VUE_APP_GITHUB_ENDPOINT}`,
	headers: {
		Accept: "application/vnd.github.v3+json",
		"Content-Type": "application/json",
		Authorization: `Bearer ${process.env.VUE_APP_GITHUB_TOKEN}`,
	},
});
export default {
	name: "TodoIssues",
    components: {
        TodoItem
    },
	data() {
		return {
			issues: [],
			todos: [],
			todo: "",
		};
	},
	methods: {
		onAddTodo() {
			this.todos.push(this.todo);
			localStorage.setItem('todos', JSON.stringify(this.todos));
			this.todo = "";
		},
        completeTodo(index) {
            this.todos.splice(index, 1);
			localStorage.setItem('todos', JSON.stringify(this.todos));
        },
		getIssues() {
			client.get("/issues").then((res) => {
				this.issues = res.data;
			});
		},
		closeIssue(index) {
            console.log(index)
			const target = this.issues[index];
			client
				.patch(`/issues/${target.number}`, {
					state: "closed",
				})
				.then(() => {
					this.issues.splice(index, 1);
				});
		},

	},
	created() {
		this.todos = JSON.parse(localStorage.getItem('todos')) || [];
		this.getIssues();
	},
};
</script>

<style>
.issues-app {
	max-width: 600px;
	margin: auto;
}

.add-issue-form {
	margin-bottom: 20px;
}

.issue-card {
	margin: 5px 0;
}

.issue-list {
	display: flex;
	flex-wrap: wrap;
}

.input-container {
	display: flex;
}

.input-container .el-button {
	display: flex;
	margin: 0 5px 0 5px;
}
</style>