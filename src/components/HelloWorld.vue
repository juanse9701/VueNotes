<template>
  <div class="hello container">
    <img alt="Vue logo" src="../assets/logo.png" />
    <h1>{{ msg }}</h1>
    <div class="mt-5 d-flex">
      <input
        type="text"
        placeholder="Write a note.."
        class="form-control mr-3"
        v-model="task"
      />
      <b-button block id="add-task" @click="addTask" class="w-25">Add</b-button>
    </div>
    <div v-if="tasks && tasks.length > 0" class="grid-task mt-5">
      <Task v-for="(task, index) in tasks" 
        :key="index" 
        :dark="task.isDark" 
        :text="task.text"
        :index="index" 
        @removeTask="handleRemoveTask"></Task>
    </div>
    <h1 class="mt-5" v-else>You have no pending Notes or Tasks, add one to start</h1>
  </div>
</template>

<script>
import Task from "./Task";

const KEY_TASK='tasks';

export default {
  name: "HelloWorld",
  props: {
    msg: String,
  },
  components: {
    Task
  },
  data() {
    return {
      tasks: [],
      task: "",
      isDark: true
    };
  },
  created() {
    this.tasks = JSON.parse(localStorage.getItem(KEY_TASK)) || []
  },
  methods: {
    addTask() {
      const newTask = {
        text: this.task,
        isDark: this.isDark
      }
      this.tasks.push(newTask)
      this.saveToLocalStorage(this.tasks)
      this.clearTask()
    },
    clearTask() {
      this.task = ""
      this.isDark = !this.isDark
    },
    handleRemoveTask(index) {
      this.tasks.splice(index, 1);
      this.saveToLocalStorage(this.tasks)
    },
    saveToLocalStorage(tasks) {
      localStorage.setItem(KEY_TASK, JSON.stringify(tasks))
    }
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.hello {
  #add-task {
    background-color: #41b883;
    border-color: #41b883;
    transition: 0.5s all;

    &:hover {
      background-color: #34495e;
    }
  }

  .grid-task {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
    gap: 15px;
  }
}
</style>
