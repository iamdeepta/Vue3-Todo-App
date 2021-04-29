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
        <div v-if="todo_text" style="margin-top: 20px">
          <span style="margin-top: 120px"
            >Make your list of <span style="color: green">ToDos</span></span
          >
        </div>
        <tr
          class="row todo_list"
          v-for="(datas, index) in todoTasks"
          :key="index"
        >
          <td style="width: 60%">
            <h6
              :ref="'text' + index"
              @click="edit(index)"
              style="cursor: pointer"
            >
              {{ index + 1 }}. {{ datas.toUpperCase() }}
            </h6>
            <form @submit.prevent="updateTask(index)">
              <input
                type="text"
                :ref="'task_input1' + index"
                class="task_input1 form-control col-md-12"
                :value="datas.toUpperCase()"
                style="display: none; text-align: center"
              />
              <span
                :ref="'input_error' + index"
                style="color: red; font-size: 12px; display: none"
                >Write Something!</span
              >
            </form>
          </td>
          <td style="width: 20%"></td>
          <td>
            <button
              :ref="'delete_btn' + index"
              class="btn btn-danger btn-sm"
              @click="deleteTask(index)"
            >
              x
            </button>
            <span :ref="'tick_btn' + index" style="display: none"> ✅ </span>
          </td>
        </tr>
      </table>
    </div>
    <Footer />
  </div>
</template>

<script>
//import Data from "../data.js";
import Footer from "./Footer.vue";
export default {
  name: "Todos",
  data() {
    return {
      taskList: null,
      updatedTaskList: null,
      todoTasks: [],
      errors: "",
      todo_text: true,
      delete_mark: "",
    };
  },
  components: {
    Footer,
  },

  methods: {
    addTask() {
      if (this.taskList != null) {
        this.todoTasks.push(this.taskList);
        this.serial = this.serial + 1;
        this.taskList = null;
        this.errors = "";
        this.todo_text = false;
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
      let x = this.$refs["text" + index];
      x.style.textDecoration = "line-through";
      x.style.color = "gray";

      let y = this.$refs["delete_btn" + index];
      y.style.display = "none";
      let z = this.$refs["tick_btn" + index];
      z.style.display = "block";
      //this.todoTasks.push(this.todoTasks[index])
      //this.todoTasks.splice(index, 1);
    },

    edit(index) {
      if (this.$refs["text" + index].style.color !== "gray") {
        this.$refs["text" + index].style.display = "none";
        this.$refs["task_input1" + index].style.display = "block";
      } else {
        this.$refs["input_error" + index].style.display = "block";
        this.$refs["input_error" + index].innerHTML = "You cannot update this!";
        setTimeout(() => {
          this.$refs["input_error" + index].style.display = "none";
        }, 2000);
      }
    },

    updateTask(index) {
      let val = this.$refs["task_input1" + index].value;
      if (val !== "") {
        this.todoTasks[index] = val;
        //console.log(this.todoTasks[index]);
        this.$refs["text" + index].style.display = "block";
        this.$refs["task_input1" + index].style.display = "none";

        this.$refs["input_error" + index].style.display = "none";
      } else {
        this.$refs["input_error" + index].style.display = "block";
      }
    },
  },
};
</script>

<style scoped>
.main {
  padding: 50px;
}
</style>