<template>
  <div class="task-item">
    <span :class="{ completed: task.completed }">{{ task.text }}</span>
    <div class="buttons">
      <button class="complete-button" @click="toggleComplete">
        <i class="fas fa-check"></i>
      </button>
      <button class="delete-button" @click="removeTask">
        <i class="fas fa-trash-alt"></i>
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "TaskItem",
  props: {
    task: {
      type: Object,
      required: true,
    },
  },
  methods: {
    toggleComplete() {
      this.$emit("toggle-complete", this.task.id);
    },
    removeTask() {
      this.$emit("remove-task", this.task.id);
    },
  },
};
</script>

<style>
.task-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 15px;
  background-color: white;
  border: 1px solid #ddd;
  border-radius: 5px;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.task-item span {
  font-size: 16px;
}

.task-item span.completed {
  text-decoration: line-through;
  color: gray;
}

.buttons {
  display: flex;
  gap: 5px;
}

.complete-button,
.delete-button {
  background-color: transparent;
  border: none;
  font-size: 16px;
  cursor: pointer;
  padding: 5px;
  transition: transform 0.2s ease;
}

.complete-button:hover {
  color: green;
  transform: scale(1.2);
}

.delete-button:hover {
  color: red;
  transform: scale(1.2);
}
</style>
