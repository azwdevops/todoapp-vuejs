<template>
  <div class="container">
    <div class="task">
      <div class="title">
        <h1>To Do List</h1>
      </div>
      <div class="form">
        <input
          type="text"
          v-model="newTask"
          placeholder="New Task"
          @keyup.enter="addTask(tasks, newTask)"
        />
        <button @click="addTask(tasks, newTask)">
          <i class="fas fa-plus"></i>
        </button>
      </div>
      <div class="taskItems">
        <ul>
          <task-item
            v-for="(task, index) in tasks"
            :key="task.id"
            :task="task"
            @remove="removeTask(index)"
            @complete="completeTask(task)"
          ></task-item>
        </ul>
      </div>
      <div class="clearBtns">
        <button @click="clearCompleted">Clear Completed</button>
        <button @click="clearAll">Clear All</button>
      </div>
      <div class="pendingTasks">
        <span>Pending Tasks: {{ inComplete }}</span>
      </div>
    </div>
  </div>
</template>

<script>
import TaskItem from "./TaskItem.vue";

export default {
  name: "Task",
  props: [
    "tasks",
    "clearCompleted",
    "clearAll",
    "inProgress",
    "addTask",
    "removeTask",
    "completeTask",
  ],
  components: {
    TaskItem,
  },
  data: () => {
    return {
      newTask: "",
    };
  },
  computed: {
    inComplete() {
      return this.tasks.filter(this.inProgress).length;
    },
  },
};
</script>