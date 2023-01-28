<template>
  <div class="App">
    <h1>{{title}}</h1>
    <InputForm 
      @addToDo="addToDo"
    />
    <Filter 
      @filter="setFilter" 
      :filter="filter"
    />
    <ul>
      <ToDoList 
        v-for="task in filterList" 
        :key="task.id" 
        :task="task" 
        @removeToDo="removeToDo" 
        @toggleCheck="toggleCheck"
        @updateToDo="updateToDo"
      />
    </ul>
  </div>
</template>


<script>
import InputForm from './components/InputForm';
import Filter from './components/Filter';
import ToDoList from './components/ToDoList';


export default {
  name: "App",
  components: {
    InputForm,
    Filter,
    ToDoList
  },

  data() {
    return {
      title: "Todo App",
      filter: "All",
      taskList: [{task: "Example1", isComplete: false , id: 1}]
    }
  },

  methods: {
    setFilter(filter) {
      this.filter = filter;
    },

    addToDo(todo) {
      let id = 1;
      if(this.taskList.length > 0) {
        id = this.taskList[this.taskList.length-1].id + 1;
        this.taskList = [...this.taskList, {task: todo, id, isComplete: false}];
      } else {
        this.taskList = [{task: todo, id, isComplete: false}];
      }
    },

    toggleCheck(id) {
      const newToDo = this.taskList.map(task => {
        if (task.id === id) {
          return {...task, isComplete: true};
        } else {
          return task;
        }
      });
      this.taskList = newToDo;
    },

    removeToDo(id) {
      const remainingToDo = this.taskList.filter(task => task.id !== id);
      this.taskList = remainingToDo;
      console.log(this.taskList);
    },

    updateToDo(id, update) {
      const updatedList = this.taskList.map(task => {
        if (task.id === id) {
          return {...task, task: update};
        } else {
          return task;
        }
      });
      this.taskList = updatedList;
    }
  },

  computed: {
    filterList() {
      if (this.filter === "All") {
        return this.taskList;
      } else {
        return this.taskList.filter(
          task => this.filter === "Active" ? !task.isComplete : task.isComplete);
      }
    }
  }

}
</script>

<style>
  @import url("https://fonts.googleapis.com/css2?family=Montserrat:wght@700&family=Varela+Round&display=swap");

  *, *::after, *::before {
    box-sizing: border-box;
    font-family: "Varela Round", sans-serif;
  }

  h1 {
    text-align: center;
    padding: 20px;
  }

  ul {
    padding: 0;
  }

  ul li {
    list-style-type: none;
  }

  input {
    height: 3em;
    width: 100%;
    padding: 5px;
  }

  .App {
    max-width: 500px;
    min-width: 300px;
    min-height: 90vh;
    margin: auto;
    padding: 20px;
    border: 1px #9e9494 solid;
    box-shadow: 2px 2px #dad5d5, -2px -1px #dad5d5;
  }
</style>
