<template>
  <ul class="filter-group">
    <li class="filter-list" v-for="(filterItem, index) in filters" :key="index">
        <button v-if="filter!==filterItem" class="filter-btn" @click="$emit('filter', filterItem)">{{filterItem}}</button>
        <button v-else-if="filter===filterItem" class="filter-btn active" @click="$emit('filter', filterItem)">{{filterItem}}</button>
    </li>
  </ul>
</template>

<script>
  export default {
    name: "InputForm",
    data() {
      return {
        input: "",
        filters: ["All", "Active", "Complete"]
      } 
    },

    props: {
      filter: {
        type: String,
        required: true
      }
    }
  }
  
</script>

<style scoped>
    .filter-group {
        display: flex;
        margin: 10px 0;
        padding: 0;
    }

    .filter-list {
        width: 100%;
    }

    .filter-btn {
        width: 100%;
        height: 30px;
        background-color: #dad5d5,;
        border: none;
        padding: 0;
        cursor: pointer;
    }

    .filter-btn:hover {
        border: 1px black solid;
    }
 
    .active {
        composes: filterBtn;
        border: 1px black solid;
    }
</style>
