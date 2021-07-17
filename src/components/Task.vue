<template>
  <div class="bg-gray-100 rounded-sm m-1 pt-3 pb-5 cursor-pointer">
    <h3 class=" flex justify-between px-2">
      {{ task.text }}
      <i @click="onDelete(task.id)" class="fas fa-times text-red-500 "></i>
    </h3>
  </div>
</template>

<script>
export default {
  name: 'Task',
  props: {
    task: Object,
  },
  methods: {
    onDelete(id) {
      //   console.log(id);
      this.$emit('delete-task', id);
    },
  },
};
</script>
