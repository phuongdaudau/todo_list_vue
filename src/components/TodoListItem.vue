<template>
    <tr>
        <td class="text-center">{{ index }}</td>
        <td>{{ task.name }}</td>
        <td class="text-center"><span v-bind:class="classLevel">{{ getLevelName}}</span></td>
        <td>
            <button 
                v-on:click="handleEdit"
                type="button" class="btn btn-warning">Edit</button>
            <button 
                v-on:click="handleDelete"
                type="button" class="btn btn-danger">Delete</button>
        </td>
    </tr>
</template>

<script>
import mapLevel from '../mocks/level'
export default {
    name: 'todo-list-item',
    props: {
        task: {type: Object, default: null},
        index: null
    },
    data(){
        return { 
            mapLevel: mapLevel
        }
    },
    computed: {
        getLevelName() {
            return this.mapLevel[this.task.level].name;
        },
        classLevel() {
            return this.mapLevel[this.task.level].class;
        }
    },
    methods: {
        handleDelete(){
            if(confirm('Bạn có muốn xóa task có tên là ' + this.task.name));
                this.$emit('handleDelete', this.task);
        },
        handleEdit() {
            this.$emit('handleEdit', this.task);
        }
    }
}
</script>

<style>
</style>