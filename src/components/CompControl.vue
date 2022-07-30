<template>
    <div class="col-12 col-lg-6">
        <div class="row">
            <control-sort
                v-bind:orderBy="orderBy"
                v-bind:orderDir="orderDir"
                v-on:handleSort="handleSort"
            />

            <control-search
            v-bind:strSearch="strSearch"
            v-on:handleSearch="handleSearch"
            />
        </div>
    </div>
</template>

<script>
import ControlSort from './ControlSort.vue'
import ControlSearch from './ControlSearch.vue'
export default{
    name: 'comp-control', 
    components: {
        ControlSort, 
        ControlSearch
    },
    props: {
        strSearch: {type: String, default: ''},
        orderBy: {type: String, default: 'name'},
        orderDir: {type: String, default: 'asc'}
    },
    data(){
        return { }
    }, 
    methods: {
        handleSearch(data) {
            console.log('handleSearch CompControl.vue');
            this.$emit('handleSearch', data);
        },
        handleSort(data) {
            console.log('handleSort CompControl.vue');
            this.$emit('handleSort', data);
        }
    }
}
</script>

<style>
</style>