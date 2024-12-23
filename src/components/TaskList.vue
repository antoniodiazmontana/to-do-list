<template>
  <div>
    <form @submit.prevent="addTask" class="task-form">
      <input
        v-model="newTaskText"
        placeholder="Add a new task..."
        class="task-input"
      />
      <button type="submit" class="task-button">Add</button>
    </form>
    <transition-group name="fade" tag="div" class="tasks">
      <TaskItem
        v-for="task in tasks"
        :key="task.id"
        :task="task"
        @toggle-complete="toggleTaskComplete"
        @remove-task="removeTask"
      />
    </transition-group>
  </div>
</template>

<script>
import TaskItem from "./TaskItem.vue";

export default {
  name: "TaskList",
  components: { TaskItem },
  data() {
    return {
      newTaskText: "",
      tasks: [],
    };
  },
  mounted() {
    this.loadTasks();
  },
  methods: {
    addTask() {
      if (this.newTaskText.trim() !== "") {
        const newTask = {
          id: Date.now(),
          text: this.newTaskText,
          completed: false,
        };
        this.tasks.push(newTask);
        this.saveTasks();
        this.newTaskText = "";
      }
    },
    toggleTaskComplete(id) {
      const task = this.tasks.find((t) => t.id === id);
      if (task) {
        task.completed = !task.completed;
        this.saveTasks();
      }
    },
    removeTask(id) {
      this.tasks = this.tasks.filter((t) => t.id !== id);
      this.saveTasks();
    },
    saveTasks() {
      localStorage.setItem("tasks", JSON.stringify(this.tasks));
    },
    loadTasks() {
      const savedTasks = localStorage.getItem("tasks");
      if (savedTasks) {
        this.tasks = JSON.parse(savedTasks);
      }
    },
  },
};
</script>

<style>
.task-form {
  display: flex;
  gap: 10px;
  margin-bottom: 20px;
}

.task-input {
  flex: 1;
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
  font-size: 16px;
}

.task-button {
  background-color: #4caf50;
  color: white;
  border: none;
  padding: 10px 15px;
  font-size: 16px;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.task-button:hover {
  background-color: #45a049;
}

.tasks {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}

.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>
