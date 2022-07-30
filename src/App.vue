<template>
	<div id="app">
		<b-container>
			<comp-title/>

			<b-row>
				<comp-control
					v-bind:strSearch="strSearch"
					v-on:handleSearch="handleSearch"
				/>

				<comp-form
					v-bind:isShowForm="isShowForm"
					v-on:toggleForm="toggleForm"
				/>
			</b-row>

			<todo-list-table
				v-bind:listTask="listTaskSearch"
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
			strSearch: ''
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
			const { strSearch } = this; //khai báo kiểu destructing es6
			var newItems = this.listTask.filter(item => {
				return item.name.toLocaleLowerCase().includes(strSearch.toLocaleLowerCase());
			});
			return newItems;

		}
	},
	methods: {
		toggleForm() {
			console.log('toggleForm App.vue');
			this.isShowForm = !this.isShowForm;
		},
		handleSearch(data){
			console.log('handleSearch app.vue');
			this.strSearch = data;
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
