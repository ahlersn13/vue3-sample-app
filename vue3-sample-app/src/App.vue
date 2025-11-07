<template>
  <div>
    <h1>Vue 3 Sample Task App</h1>
    <input v-model="newTask" placeholder="Add a new task" />
    <button @click="addTask">Add Task</button>

    <ul>
      <li v-for="task in tasks" :key="task.id">
        <label>
          <input type="checkbox" v-model="task.completed" />
          <span :style="{ textDecoration: task.completed ? 'line-through' : 'none' }">{{ task.text }}</span>
        </label>
        <button @click="removeTask(task.id)">Remove</button>
      </li>
    </ul>

    <p>Tasks Completed: {{ completedTasks }} / {{ tasks.length }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newTask: '',
      tasks: [
        { id: 1, text: 'Learn Vue 3', completed: false },
        { id: 2, text: 'Create a sample app', completed: true }
      ]
    };
  },
  methods: {
    addTask() {
      if (this.newTask.trim()) {
        this.tasks.push({
          id: this.tasks.length + 1,
          text: this.newTask.trim(),
          completed: false
        });
        this.newTask = '';
      }
    },
    removeTask(id) {
      this.tasks = this.tasks.filter(task => task.id !== id);
    }
  },
  computed: {
    completedTasks() {
      return this.tasks.filter(task => task.completed).length;
    }
  }
};
</script>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
