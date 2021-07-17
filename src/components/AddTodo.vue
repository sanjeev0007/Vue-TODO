<template>
  <form @submit="onSubmit" class="mb-10">
    <div class="mb-4 flex px-2">
      <label class="mr-4">Task</label>
      <input
        class="w-full"
        type="text"
        v-model="text"
        name="text"
        placeholder="Add Task"
      />
    </div>
    <!-- {{ text }} -->
    <input
      type="submit"
      value="Save Task"
      class="bg-black text-white w-full p-2 rounded-2xl cursor-pointer hover:shadow-xl outline-none"
    />
  </form>
</template>

<script>
export default {
  name: 'AddTodo',
  data() {
    return {
      text: '',
    };
  },
  methods: {
    onSubmit(e) {
      e.preventDefault();
      if (!this.text) {
        alert('Please add a task');
        return;
      }

      const newTask = {
        id: Math.floor(Math.random() * 100000000),
        text: this.text,
      };

      this.$emit('add-task', newTask);
      this.text = '';
    },
  },
};
</script>
