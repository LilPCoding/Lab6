<template>
  <h1>{{ title }}</h1>
  <ul>
    <li v-for="task in task" :key="task.id">
      {{ task.id }}. {{ task.name }}
      
      <div v-if="task.finished">
        <button>Delete Task</button> 
      </div>
      
      </li>
  </ul>
</template>

<script>
export default {
  data() {
    return {
      title: "My To-Do App",
      task: [
        { id: 1, name: "Learn VUE js", finished: true },
        { id: 2, name: "Build a Vue App", finished: false },
        { id: 3, name: "Build Todo App", finished: false },
      ],
    };
  },
};
</script>

<style></style>
