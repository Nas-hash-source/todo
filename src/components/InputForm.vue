<template>
  <form class="input-form" @submit.prevent="handleSubmit()">
    <input class="input-primary" type="text" v-model.trim="input" autocomplete="off" autofocus>
    <button class="btn-primary" @submit.prevent="handleSubmit()">Add</button>
  </form>
</template>

<script>
  export default {
    name: "InputForm",
    data() {
      return {
        input: ""
      }
    },

    methods: {
      handleSubmit() {
        if(this.input) {
          this.$emit('addToDo', this.input);
          this.input = "";
        }
      }
    }
  }
  
</script>

<style scoped>
  .input-form {
    display: flex;
  }

  .input-primary {
      width: 100%;
      height: 40px; 
      padding: 15px;
  }

  .btn-primary {
      color: white;
      background-color: black;
      width: 100px;
      height: 40px;
      border: none;
  }

  .btn-primary:hover {
      background-color: #8a8787;
  }
</style>
