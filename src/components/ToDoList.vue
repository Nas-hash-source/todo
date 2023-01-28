<template>
  <li v-if="!editable" class="todo">
    <form class="form">
      <input class="checkbox" type="checkbox" :checked="task.isComplete" :id="task.id" @change="$emit('toggleCheck', task.id)" />
      <label class="label" :for="task.id">{{task.task}}</label>
    </form>
    <div class="btn-wrapper">
      <button ref="editButton" class="btn" @click="editable=true; $nextTick(() => $refs.updateRef.focus())">Edit</button>
      <button 
        class="btn delete" 
        @click="$emit('removeToDo', task.id)"
      >
        Delete
      </button>
    </div>
  </li>
  <li v-else-if="editable" class="todo">
    <form class="form" @submit="$emit('updateToDo', task.id, update)">
      <input class="update" ref="updateRef" type="text" :id="task.id" v-model.trim="update" autocomplete="off" />
    </form>
    <div class="btn-wrapper">
      <button class="btn save" @click="$emit('updateToDo', task.id, update); editable=false; focusOnEdit()">Save</button>
      <button class="btn" @click="editable=false; focusOnEdit()" >Cancel</button>
    </div>
  </li>
</template>

<script>
  export default {
    name: "ToDoList",
    data() {
      return {
        editable: false,
        update: this.task.task,
      }
    },
    props: {
      task: Object
    },

    methods: {
      focusOnEdit() {
        this.$nextTick(() => {
          const editButton = this.$refs.editButton;
          editButton.focus();
        });
      }
    }
  };
</script>

<style scoped>
  .todo {
    display: block;
    padding: 10px 0;
  }

  .checkbox {
      height: 20px;
      width: 20px;
      margin: 0;
  }

  .btn-wrapper {
      display: flex;
      gap: 10px;
      padding: 10px 0;
  }

  .form {
      display: flex;
      gap: 10px;
      align-items: center;
  }

  .update {
      width: 100%;
      height: 35px;
  }

  .label {
      height: 15px;
  }

  .btn {
      height: 30px;
      width: 100%;
      border: none;
      cursor: pointer;
  }

  .save {
      background-color: green;
      color: white;
  }

  .delete {
      background-color: tomato;
      color: #000000;
  }
</style>