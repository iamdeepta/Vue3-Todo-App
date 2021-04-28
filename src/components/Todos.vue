<template>
  <div class="card main container col-md-4">
    <div class="input">
      <form @submit.prevent="addTask">
        <div class="row">
          <input
            type="text"
            class="task_input form-control col-md-10"
            v-model="taskList"
          />
          <button type="submit" class="btn btn-primary col-md-1 ml-1">+</button>
        </div>
        <p style="color: red; font-size: 12px; margin-top: 13px">
          {{ errors }}
        </p>
      </form>
    </div>
    <div class="row todo_list" v-for="(datas, index) in todoTasks" :key="index">
      <h6 :id="'text' + index" :ref="'text' + index">
        {{ index + 1 }}. {{ datas.toUpperCase() }}
      </h6>
      <button class="btn btn-danger btn-sm" @click="deleteTask(index)">
        -
      </button>
    </div>
  </div>
</template>

<script>
//import Data from "../data.js";
export default {
  name: "Todos",
  data() {
    return {
      taskList: null,
      todoTasks: [],
      errors: "",
    };
  },

  methods: {
    addTask() {
      if (this.taskList != null) {
        this.todoTasks.push(this.taskList);
        this.serial = this.serial + 1;
        this.taskList = null;

        this.errors = "";
      } else if (this.taskList == null) {
        this.errors = "Please write something!";
        setTimeout(() => {
          this.errors = "";
        }, 3000);
      }
    },
    deleteTask(index) {
      //let x = this.todoTasks.indexOf(this.todoTasks[index]);
      //this.$refs.style.textDecoration = "line-through";

      let x = document.getElementById("text" + index);
      x.style.textDecoration = "line-through";
      //this.todoTasks.splice(index, 1);
    },
  },
};
</script>

<style>
.main {
  padding: 50px;
}
</style>