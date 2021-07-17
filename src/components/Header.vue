<template>
  <header>
    <h1 class="mb-5 font-bold text-xl">{{ title }}</h1>
  </header>
</template>

<script>
export default {
  name: 'Header',
  props: {
    title: String,
  },
};
</script>
