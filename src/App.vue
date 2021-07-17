<template>
  <div class="flex justify-center min-h-300 mt-8">
    <div class="max-w-sm mt-4 border border-blue-500 rounded-lg p-4">
      <Header title="TODO List" />
      <AddTodo @add-task="addTask" />
      <Tasks @delete-task="deleteTask" :tasks="tasks" />
    </div>
  </div>
</template>

<script>
import Header from './components/Header.vue';
import Tasks from './components/Tasks.vue';
import AddTodo from './components/AddTodo.vue';
import './index.css';

export default {
  name: 'App',
  components: {
    Header,
    Tasks,
    AddTodo,
  },
  data() {
    return {
      tasks: [
        {
          id: 1,
          text: 'demo',
        },
      ],
    };
  },
  created() {
    this.getTasks();
  },
  methods: {
    getTasks() {
      localStorage.getItem('tasks');
      this.tasks = JSON.parse(localStorage.getItem('tasks'));
    },
    deleteTask(id) {
      if (confirm('Do you want to delete this task?')) {
        let tasks = this.tasks.filter((task) => task.id !== id);
        localStorage.setItem('tasks', JSON.stringify(tasks));
        this.tasks = tasks;
      }
    },
    addTask(task) {
      let tasks = [...this.tasks, task];
      localStorage.setItem('tasks', JSON.stringify(tasks));
      this.tasks = tasks;
    },
  },
};
</script>
