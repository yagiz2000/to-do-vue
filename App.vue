<template>
  <div class="app">
    <SearchBar @messageString="handleMessageString" />
    <Todos @changedToDoS2="handleChangedToDos2" @changedToDos="handleChangedToDos" @deletedToDos="handleTodos" v-bind:todos="todos" />
  </div>
</template>

<script>
import SearchBar from "./components/SearchBar";
import Todos from "./components/Todos";
 export default {
  name: "App",
  components: {
    SearchBar,
    Todos  
    },
  data() {
    return {
      todos: [],
      newToDo: null,
    };
  },
  methods: {
    handleMessageString(message) {
      console.log(message);
      if (message === "") {
        return;
      }
      let todo = {
        message: message,
        status: false,
        isDone:false
      };
      this.todos.push(todo);
      let newToDos = this.todos;
      this.saveToDos(newToDos);
    },
    handleTodos(newToDos) {
      this.todos = newToDos;
      //console.log("hello "+newToDos);
      this.saveToDos(newToDos);
    },
    saveToDos(newToDos) {
      
      let data = JSON.stringify(newToDos);
      localStorage.setItem("todos", data);
      
    },
    handleChangedToDos(changedToDos){
      this.saveToDos(changedToDos);
    }, 
    handleChangedToDos2(changedToDos){
      this.saveToDos(changedToDos);
    }
  },
  mounted() {
    //Sayfa yüklendiğinde çalışacak kısım
    if (localStorage.getItem("todos")) {
      try {
        this.todos = JSON.parse(localStorage.getItem("todos"));
      } catch (e) {
        alert("something went wrong " + e);
      }
    }
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
