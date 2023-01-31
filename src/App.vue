<template>
  <img :src="logoURL" :alt="logoCaption" width="200" height="200" />

  <h1>{{ title }}</h1>

  <div>
    <span
      >You have {{ allTask }} {{ allTask > 1 ? "task" : "task" }} at the moment
    </span>
    <br />

    <input
      type="text"
      v-model="newTask"
      placeholder="Add a new task"
      @keyup.enter="addTask"
    />

    <button @click="addTask" :disabled="newTask.length < 1">Add Task</button>
  </div>

  <div v-if="newTask.length > 0">
    <h3>New Task Preview</h3>
    <p>{{ newTask }}</p>
  </div>

  <ul>
    <li
      v-for="(task, index) in latest"
      :key="task.id"
      @click="finishTask(task)"
      :class="{ strikeout: task.finished }"
    >
      {{ index + 1 }}. {{ task.name }}

      <div v-if="task.finished">
        <button @click="removeTask(task.id)">Delete Task</button>
      </div>

      <div v-else-if="task.edit">
        <button>Edit Task</button>
      </div>
    </li>
  </ul>
</template>

<script>
export default {
  data() {
    return {
      title: "My to Do app",
      newTask: "",
      logoURL: "https://unsplash.com/photos/0J8thHZfosE",
      logoCaption: "this is caption",
      tasks: [
        { id: 1, name: "Learn vue js", finished: true },
        { id: 2, name: "Build a vue app", finished: false },
        { id: 3, name: "Build todo app", finished: false },
      ],
    };
  },
  methods: {
    addTask() {
      if (this.newTask.length < 1) return;

      this.tasks.push({
        id: this.tasks.length + 1,
        name: this.newTask,
        finished: false,
      });

      this.newTask = "";
    },
    finishTask(task) {
      task.finished = !task.finished;
    },
    removeTask(taskID) {
      this.tasks = this.tasks.filter((task) => {
        return task.id !== taskID;
      });
    },
  },
  computed: {
    allTask() {
      return this.tasks.length;
    },
    latest() {
      return [...this.tasks].reverse();
    },
  },
};
</script>

<style>
.strikeout {
  text-decoration: line-through;
}
</style>
