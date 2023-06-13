<template>
  <nav class="filter-nav">
    <button @click="filterBy('all')">all</button>
    <button @click="filterBy('completed')">completed</button>
    <button @click="filterBy('ongoing')">ongoing</button>
  </nav>
</template>

<script>
export default {
    methods:{
        filterBy(value){
            this.$emit('filter',value);
        }
    }
}
</script>

<style>
    .filter-nav button{
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
</style>