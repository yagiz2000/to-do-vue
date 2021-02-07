<template>
  <div class="cards">
    <div class="container mt-3 d-flex flex-wrap justify-content-space-evenly">
      <div v-for="(todo, index) in todos" :key="index" ref="index" class="row">
        <div class="col-md ">
          <div class="card ml-2 me-3 mt-2" style="width: 18rem;">
            <div class="card-body align-items">
              <input
                class="form-control mb-2"
                v-model="todo.message"
                v-if="todo.status"
              />
              <h6 v-else class="card-title text-center">{{ todo.message }}</h6>

              <div class="d-flex flex-row">
                <a
                  href="#"
                  @click="changeOnChange(index)"
                  class="btn btn-primary me-3"
                  >Değiştir</a
                >
                <a
                  v-on:click="deleteToDo"
                  href="#"
                  @click="removeCard(index)"
                  class="btn btn-danger"
                >
                  Sil</a
                >
                <label class="checkbox mx-2 mt-3" style="text-align:right">
                  <input
                    v-if="todo.isDone"
                    @click="isDoneChanged(index)"
                    v-model="todo.isDone"
                    type="checkbox"
                    class="checkbox"
                    checked  
                  />
                   <input
                    v-else
                    @click="isDoneChanged(index)"
                    v-model="todo.isDone"
                    type="checkbox"
                    class="checkbox"
                  />Yapıldı
                </label>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Todos",
  data() {
    return {
      /*  onChange: false, */
    };
  },
  props: {
    todos: Array,
  },
  methods: {
    removeCard(index) {
      let newToDos = this.todos;
      //console.log(newToDos)
      newToDos.splice(index, 1);
      this.$emit("deletedToDos", newToDos);
      //console.log(newToDos)
    },
    changeOnChange(index) {
      if (!this.todos[index].status) {
        this.todos[index].status = true;
      } else {
        this.todos[index].status = false;
        console.log(this.todos[index].message);
        let newTodos = this.todos;
        console.log(newTodos);
        this.$emit("changedToDos", newTodos);
      }
    },
    isDoneChanged(index) {
      //console.log(this.todos[index].isDone);
      if (this.todos[index].isDone === false) {
        console.log("ilk blok çalıştı");
        this.todos[index].isDone = true;
        let newToDos = this.todos;
        return this.$emit("changedToDoS2", newToDos);
      }
      if (this.todos[index].isDone === true) {
        this.todos[index].isDone = false;
        let newToDos = this.todos;
        return this.$emit("changedToDoS2", newToDos);
      }
    },
  },
};
</script>

<style>
.checkbox{
  width: 30%;
}
.card-body{
  background-color:peru;
  border-radius: 5px;
}
</style>
