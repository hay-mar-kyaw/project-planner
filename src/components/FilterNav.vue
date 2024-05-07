<template>
    <div>
        <nav class="filter-nav"> 
            <button @click="filterValue('all')" :class="{active:current==='all'}">All</button>
            <button @click="filterValue('complete')" :class="{active:current==='complete'}">Completed</button>
            <button @click="filterValue('ongoing')" :class="{active:current==='ongoing'}">Ongoing</button>
        </nav>
    </div>
</template>

<script>
    export default {
        props:['current'],
        data(){
            return{
                
            }
        },
        methods:{
            filterValue(value){
                this.$emit("current",value);
            }
        }
    }
</script>

<style scoped>
    .filter-nav button {
        background: none;
        border: none;
        color: #bbb;
        outline: none;
        font-size: 12px;
        text-transform: uppercase;
        margin-right: 10px;
        letter-spacing: 1px;
        font-weight: bold;
        cursor: pointer;
    }
    button.active {
        color: #333;
    }
</style>