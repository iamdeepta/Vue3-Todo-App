<template>
  <div
    class="card main container col-md-4"
    style="box-shadow: 1px 2px 2px 2px lightgray"
  >
    <div
      class="card-header"
      style="background-color: white; font-size: 28px; font-weight: bold"
    >
      <span style="color: green">Vue</span> ToDos
    </div>
    <div class="card-body">
      <div class="input">
        <form @submit.prevent="addTask">
          <div class="row">
            <input
              type="text"
              class="task_input form-control col-md-10"
              v-model="taskList"
            />
            <button type="submit" class="btn btn-primary col-md-1 ml-1">
              +
            </button>
          </div>
          <p style="color: red; font-size: 12px; margin-top: 13px">
            {{ errors }}
          </p>
        </form>
      </div>
      <table class="table">
        <tr
          class="row todo_list"
          v-for="(datas, index) in todoTasks"
          :key="index"
        >
          <td style="width: 60%">
            <h6 :id="'text' + index" :ref="'text' + index">
              {{ index + 1 }}. {{ datas.toUpperCase() }}
            </h6>
          </td>
          <td style="width: 20%"></td>
          <td>
            <button
              :id="'delete_btn' + index"
              class="btn btn-danger btn-sm"
              @click="deleteTask(index)"
            >
              x
            </button>
            <span :id="'tick_btn' + index" style="display: none"> ✅ </span>
          </td>
        </tr>
      </table>
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
      //let a = this.todoTasks.indexOf(this.todoTasks[index]);
      //this.$refs.style.textDecoration = "line-through";
      let x = document.getElementById("text" + index);
      x.style.textDecoration = "line-through";
      x.style.color = "gray";
      let y = document.getElementById("delete_btn" + index);
      y.style.display = "none";
      let z = document.getElementById("tick_btn" + index);
      z.style.display = "block";
      //this.todoTasks.push(this.todoTasks[index])
      //this.todoTasks.splice(index, 1);
    },
  },
};
</script>

<style scoped>
.main {
  padding: 50px;
}
</style>