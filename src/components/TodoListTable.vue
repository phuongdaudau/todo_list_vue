<template>
    <div class="panel panel-success">
        <div class="panel-heading">List Task</div>
        <table class="table table-hover ">
            <thead>
                <tr>
                    <th style="width: 10%" class="text-center">#</th>
                    <th>Task</th>
                    <th style="width: 20%" class="text-center">Level</th>
                    <th style="width: 160px">Action</th>
                </tr>
            </thead>

            <tbody v-if="listTask.length !== 0">
                <todo-list-item
                v-for="(task, index) in listTask"
                v-bind:key="task.id"
                v-bind:task="task"
                v-bind:index="index +1"
                v-on:handleDelete="handleDelete"
                v-on:handleEdit="handleEdit"
                />
            </tbody>
            <tbody v-else>
                <tr>
                    <td colspan="4"><h3>List Empty</h3></td>
                </tr>
            </tbody>

        </table>
    </div>
</template>

<script>
import TodoListItem from './TodoListItem.vue'
export default {
    name: 'todo-list-table',
    props: {
        listTask: {type: Array, default: []}
    },
    components: {
        TodoListItem
    },
    data(){
        return {

        }
    },
    methods: {
        handleDelete(taskDelete) {
            console.log('handleDelete todoListTable.vue');
            this.$emit('handleDelete', taskDelete);
        },
        handleEdit(taskEdit){
            this.$emit('handleEdit', taskEdit);
        }
    }
}
</script>