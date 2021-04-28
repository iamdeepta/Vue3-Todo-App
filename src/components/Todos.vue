<template>
  <div class="main container col-md-4">
    <div class="input">
      <form @submit.prevent="addTask">
        <div class="row">
          <input
            type="text"
            class="task_input form-control col-md-6"
            v-model="taskList"
          />
          <button class="btn btn-primary col-md-4">+</button>
        </div>
        <p style="color: red; font-size: 12px; margin-top: 13px">
          {{ errors }}
        </p>
      </form>
    </div>
    <div class="todo_list" v-for="datas in todoTasks" :key="datas">
      {{ datas.toUpperCase() }}
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
        this.taskList = null;

        this.errors = "";
      } else if (this.taskList == null) {
        this.errors = "Please write something!";
        setTimeout(() => {
          this.errors = "";
        }, 3000);
      }
    },
  },
  // updated() {
  //   if (this.taskList == null) {
  //     this.errors = "Please write something!";
  //   }
  // },

  // created() {
  //   this.todoTasks = Data;
  // },
};
</script>

<style></style>