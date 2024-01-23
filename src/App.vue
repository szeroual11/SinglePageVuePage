<template>
  <div id="app">
    <h1>to do app</h1>
    <input id="new-task" v-model="newTask" type="text" placeholder="Add Element" @keyup.enter="addTask"/>
    <button id="add-task" @click="addTask()">Add</button>
    <div id="task-counter">Total tasks: {{totalTasks}} </div>
    <ul id="task-list">
      <li v-for="task of tasks" :key="task.connect">
        <input type="checkbox" v-model="task.completed"/>
        <span :class="{completed: task.completed}">{{task.content}}</span>
        <button @click="deleteTask(task)">Delete</button>
      </li>
    </ul>
  </div>
</template>

<script>
let id=0;
export default {
  name: 'App',
  data() {
    return {
      newTask: "",
      tasks: [],
    }
  },
  methods: {
    addTask() {
      if(this.newTask.trim()) {
        this.tasks = [...this.tasks,
          {content: this.newTask, completed: false, id: id++}];
        this.newTask = "";
      }
    },
    deleteTask(task) {
      this.tasks = this.tasks.filter((t) => t !== task);
    }
  },
  computed: {
    totalTasks() {
      return this.tasks.length;
    }
  }
}
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
.completed {
  text-decoration: line-through
}
</style>
