<template>
  <div id="app">
    <task
      v-bind:tasks="tasks"
      @clear-all-tasks="clearAll"
      @clear-completed="clearCompleted"
      :inProgress="inProgress"
      :clearCompleted="clearCompleted"
      :clearAll="clearAll"
      :addTask="addTask"
      :removeTask="removeTask"
      :completeTask="completeTask"
    ></task>
  </div>
</template>

<script>
import Task from "./components/Task.vue";

export default {
  name: "App",
  components: {
    Task,
  },
  data() {
    return {
      tasks: [
        {
          id: 1,
          title: "Learn Vue Js",
          completed: false,
        },
        {
          id: 2,
          title: "Watch netflix",
          completed: true,
        },
        {
          id: 3,
          title: "Go shopping",
          completed: false,
        },
        {
          id: 4,
          title: "Learn Guitar",
          completed: false,
        },
        {
          id: 5,
          title: "Send email",
          completed: true,
        },
      ],
    };
  },
  methods: {
    clearAll() {
      this.tasks = [];
    },
    isCompleted(task) {
      return task.completed;
    },
    inProgress(task) {
      return !this.isCompleted(task);
    },
    clearCompleted() {
      this.tasks = this.tasks.filter(this.inProgress);
    },
    addTask(tasks, newTask) {
      if (newTask) {
        tasks.push({
          title: newTask,
          completed: false,
        });
      }
    },
    removeTask(index) {
      this.tasks.splice(index, 1);
    },
    completeTask(task) {
      task.completed = !task.completed;
    },
  },
};
</script>