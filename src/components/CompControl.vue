<template>
    <div class="col-12 col-lg-6">
        <div class="row">
            <control-sort/>

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
        strSearch: {type: String, default: ''}
    },
    data(){
        return { }
    }, 
    methods: {
        handleSearch(data) {
            console.log('handleSearch CompControl.vue');
            this.$emit('handleSearch', data);
        }
    }
}
</script>

<style>
</style>