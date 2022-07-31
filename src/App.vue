<template>
	<div id="app">
		<b-container>
			<comp-title/>

			<b-row>
				<comp-control
					v-bind:strSearch="strSearch"
					v-bind:orderBy="orderBy"
					v-bind:orderDir="orderDir"
					v-on:handleSearch="handleSearch"
					v-on:handleSort="handleSort"
				/>

				<comp-form
					v-bind:isShowForm="isShowForm"
					v-on:toggleForm="toggleForm"
					v-bind:taskSelected="taskSelected"
					v-on:handleAddNewTask="handleAddNewTask"
					v-on:handleEditTaskById="handleEditTaskById"
				/>
			</b-row>

			<todo-list-table
				v-bind:listTask="listTaskSort"
				v-on:handleDelete="handleDelete"
				v-on:handleEdit="handleEdit"
			/>
		</b-container>
	</div>
</template>

<script>
import CompTitle from './components/CompTitle.vue'
import CompControl from './components/CompControl.vue'
import CompForm from './components/CompForm.vue'
import TodoListTable from './components/TodoListTable.vue'

import listTask from './mocks/tasks'

export default {
	name: 'app',
	data() {
		return {
			isShowForm: false,
			listTask: listTask,
			strSearch: '',
			orderBy: 'name',
			orderDir: 'asc',
			taskSelected: null
		}
	},
	components: {
		CompTitle,
		CompControl, 
		CompForm,
		TodoListTable
	},
	computed: {
		listTaskSearch() {
			const { strSearch } = this; //destructing
			var newItems = this.listTask.filter(item => {
				return item.name.toLocaleLowerCase().includes(strSearch.toLocaleLowerCase());
			});
			return newItems;
		},
		listTaskSort() {
			var listTask = [...this.listTaskSearch]; // spread operator
			listTask.sort(this.compareSort);

			return listTask;
		}
	},
	methods: {
		toggleForm() {
			if(this.isShowForm) this.taskSelected = null;
			console.log('toggleForm App.vue');
			this.isShowForm = !this.isShowForm;
		},
		handleSearch(data){
			console.log('handleSearch app.vue');
			this.strSearch = data;
		},
		handleSort(data){
			this.orderBy = data.orderBy;
			this.orderDir = data.orderDir;
			console.log('handleSort app.vue', data);
		},
		compareSort(a, b){
			var numberSort = this.orderDir == 'asc' ? -1 :  1;

			if(a[this.orderBy] < b[this.orderBy]) return numberSort;
			else if(a[this.orderBy] > b[this.orderBy]) return numberSort * (-1);
			return 0;
		},
		handleDelete(taskDelete) {
			this.listTask = this.listTask.filter(item => item.id != taskDelete.id);
			console.log('handleDelete App.vue: ', taskDelete);
		},
		handleAddNewTask(newTask){
			this.listTask.push(newTask);
			console.log('handleAddTask app.vue',newTask);
		},
		handleEdit(taskEdit) {
			this.isShowForm = true;
			this.taskSelected = taskEdit;
		},
		handleEditTaskById(taskEdit){
			let index = this.listTask.findIndex(item => item.id === taskEdit.id);

			if(index !== -1) {
				this.listTask.splice(index, 1, taskEdit);
				this.toggleForm();
			}
		}
		
	}
}
</script>

<style>

body {
    padding: 100px 0;
}
.table>tbody>tr>td, .table>tbody>tr>th, .table>tfoot>tr>td, .table>tfoot>tr>th, .table>thead>tr>td, .table>thead>tr>th {
    vertical-align: middle;
}

.container > .row {
    margin-top: 20px;
    margin-bottom: 30px;
}

span.badge-medium {
	padding: 11px 10px;
    margin: 0px 8px;
    font-size: 16px;
    display: inline-block;
    vertical-align: top;
}

@media (max-width: 992px) {
    .add-task {
        margin-top: 50px;
    }
}

</style>
