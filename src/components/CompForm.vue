<template>
    <b-col cols="12" lg="6">
        <form-add
            v-bind:isShowForm="isShowForm"
            v-on:handleToggleForm="handleToggleForm"
        />
        
        <form  v-if="isShowForm" action="" method="POST" class="form-inline justify-content-between">
            <div class="form-group">
                <label class="sr-only" for="">label</label>
                <input v-model="taskname" type="text" class="form-control" placeholder="Task Name" />
            </div>
            <div class="form-group">
                <label class="sr-only" for="">label</label>
                <select v-model="level" name="ds" class="form-control" required="required">
                    <option value="0">Small</option>
                    <option value="1">Medium</option>
                    <option value="2">High</option>
                </select>
            </div>

            <button 
                v-if="taskSelected === null"
                v-on:click="handleAddNew"
                type="button" class="btn btn-primary">Submit</button>
            <button 
                v-else
                v-on:click="handleEditTask"
                type="button" class="btn btn-primary">Update</button>
            <button 
                v-on:click="handleCancel"
                type="button" class="btn btn-secondary">Cancel</button>
        </form>
    </b-col>
</template>

<script>
import FormAdd from './FormAdd.vue';
const { v4: uuidv4 } = require('uuid');

export default {
    name: 'comp-form',
    components: {
        FormAdd
    }, 
    props: {
        isShowForm: {type: Boolean, default: false },
        taskSelected: {type: Object, default: null}
    },
    data() {
        return {
            taskname: '', 
            level: 0
        }
    }, 
    watch: {
        taskSelected: function(newData, oldData){
            if(newData != null){
                this.taskname = newData.name;
                this.level - newData.level;
            }
            console.log("watcher taskSelected", newData, oldData);
        }
    },
    methods: {
        handleToggleForm(){
            console.log("handleAddTag CompForm.vue");
            this.$emit('toggleForm');
        },
        handleAddNew() {
            let objTask = {
                id: uuidv4(),
                name: this.taskname,
                level: parseInt(this.level)
            }
            console.log('handleAddNew', objTask);
            this.$emit('handleAddNewTask', objTask);
            this.handleCancel();
        },
        handleCancel() {
            this.$emit('toggleForm');
            this.handleResetData();
        },
        handleResetData() {
            this.taskname = '';
            this.level = 0;
        },
        handleEditTask() {
            let objEditTask = {
                id: this.taskSelected.id,
                name: this.taskname,
                level: parseInt(this.level)
            }
            this.$emit('handleEditTaskById', objEditTask);
            this.handleResetData();
        }
    }
}
</script>

<style>
</style>